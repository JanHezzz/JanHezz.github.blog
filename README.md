# JanHezz.github.blog
关于HttoClient的使用
 
/ /使用Get方式请求
 String city = params[0];
        //接口地址
         String JUHE_URL_ENVIRONMENT_AIR_PM =
                "http://www.weather.com.cn/data/cityinfo/101010100.html";
        //1.创建HttpClient
        HttpClient httpClient = new DefaultHttpClient();
        //2.创建请求方式
        HttpGet httpRequest=null;
        //3.设置请求头
        ArrayList<NameValuePair> headerList = new ArrayList<NameValuePair>();
        headerList.add(new BasicNameValuePair("Content-Type", "text/html; charset=utf-8"));
        httpRequest.addHeader(headerList.get(0).getName(),
                headerList.get(0).getValue());
        String targetUrl = JUHE_URL_ENVIRONMENT_AIR_PM;
        //添加请求参数
        //参数列表
        ArrayList<NameValuePair> paramList = new ArrayList<NameValuePair>();
        paramList.add(new BasicNameValuePair("city", city));
      for (int i = 0; i < paramList.size(); i++) {
            NameValuePair nowPair = paramList.get(i);
            String value = nowPair.getValue();
            try {
                //转码
                value = URLEncoder.encode(value, "UTF-8");
            } catch (Exception e) {
            }
            if (i == 0) {
                targetUrl += ("?" + nowPair.getName() + "=" + value);
            } else {
                targetUrl += ("&" + nowPair.getName() + "=" + value);
            }
        }
        //给请求方式赋值
        httpRequest = new HttpGet(targetUrl);
        //创建 HttpResponse对象
        HttpResponse httpResponse = null;
        try {
            httpResponse = httpClient.execute(httpRequest);
        } catch (IOException e) {
            e.printStackTrace();
        }
        //判断是否连接上
        if (httpResponse.getStatusLine().getStatusCode() == 200) {
            String strResult = null;
            try {
                //得到请求数据
                strResult = EntityUtils.toString(httpResponse.getEntity());
                Log.d("Result",strResult);
            } catch (IOException e) {
                e.printStackTrace();
            }
            return strResult;
            } else {
            Log.d("HTTP","未连接上");
                return null;
            }
																					 

        
    
