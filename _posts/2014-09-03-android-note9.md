---
layout: post
title: 项目中的Http的操作
category: android
description: 从Request,Cookie,User-Agent,Response等几方面简述项目中的一些Http操作
keywords: android, http
---


##Request##
###一般请求###
项目中使用Volley作为统一的请求库，从服务端返回的数据统一使用json进行了编码，所以App封装了GsonRequest类来统一处理请求（部分涉及文件操作的请求除外）

```java
public class GsonRequest<T> extends Request<T> {

	private final Gson mGson = new Gson();
	private final Class<T> mClazz;
	private final Listener<T> mListener;
	private final Map<String, String> mHeaders;
	private final Map<String, String> mParams;

	public GsonRequest(String url, Class<T> clazz, Listener<T> listener, ErrorListener errorListener, Map<String, String> params) {
		this(Method.POST, url, clazz, null, listener, errorListener, params);
	}

	public GsonRequest(int method, String url, Class<T> clazz, Map<String, String> headers, Listener<T> listener, ErrorListener errorListener, Map<String, String> params) {
		super(method, url, errorListener);
		this.mClazz = clazz;
		this.mHeaders = headers;
		this.mListener = listener;
		this.mParams = params;
	}

	@Override
	protected Map<String, String> getParams() throws AuthFailureError {
		return mParams;
	}

	@Override
	public Map<String, String> getHeaders() throws AuthFailureError {
		return mHeaders;
	}

	@Override
	protected void deliverResponse(T response) {
		mListener.onResponse(response);
	}

	@Override
	protected Response<T> parseNetworkResponse(NetworkResponse response) {
		try {
			GlobalApp.getInstance().checkSessionCookie(response.headers);
			String json = new String(response.data, HttpHeaderParser.parseCharset(response.headers));
			return Response.success(mGson.fromJson(json, mClazz), HttpHeaderParser.parseCacheHeaders(response));
		} catch (UnsupportedEncodingException e) {
			return Response.error(new ParseError(e));
		} catch (JsonSyntaxException e) {
			return Response.error(new ParseError(e));
		}
	}
}
```

Gson为Google官方用来解析json的工具，通过GsonRequest将json字符串转为Android中的对象。
具体调用如下（以登录为例）：
```java
executeRequest(new GsonRequest<UniversalReturn>(Request.Method.POST, MAPI.APIS.get("NORMALLOGIN"), UniversalReturn.class, GlobalApp.getInstance().getHeader(LoginAty.this), normalLoginResponseListener(), errorListener(), dataMap));
```

其中UniversalReturn为通用返回对象类，具体的回调在normalResponseLister()中进行处理：
```java
private Response.Listener<UniversalReturn> normalLoginResponseListener() {
	return new Response.Listener<UniversalReturn>() {
		@Override
		public void onResponse(final UniversalReturn response) {
			TaskUtils.executeAsyncTask(new AsyncTask<Object, Object, Object>() {
				@Override
				protected Object doInBackground(Object... params) {
					return null;
				}

				@Override
				protected void onPostExecute(Object o) {
	
					if ("1".equals(response.ret)) {
						Message msg = Message.obtain();
						msg.what = LOGIN_SUCCESS;
						loginHandler.sendMessage(msg);
					} else {
						Message msg = Message.obtain();
						msg.what = LOGIN_ERROR;
						msg.obj = response.err_msg;
						loginHandler.sendMessage(msg);
					}
					super.onPostExecute(o);
				}
			});
		}
	};
}
```

