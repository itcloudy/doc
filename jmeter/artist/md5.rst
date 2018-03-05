==============
md5加密
==============

加密代码
---------
	文件名为：ArtistMD5.java
.. code-block:: java
	
	package com.hechihan;
	
	import java.math.BigInteger;
	import java.security.MessageDigest;
	import java.util.*;

	public class ArtistMD5 {
	    public static String getSignKey(Map<String,String[]> map,String appId,String appSecret,
	                                    String accessToken,String requestMethod,String requestUrl){
	        map.put("appId",new String[]{appId});
	        if (!accessToken.equalsIgnoreCase("")){
	            map.put("accessToken",new String[]{accessToken});
	        }
	        List<String> keyList = new ArrayList<String>();
	        for(String key:map.keySet()){
	            keyList.add(key);
	        }
	        Collections.sort(keyList);
	        StringBuilder signSb = new StringBuilder(requestMethod.toUpperCase() + requestUrl);
	        for(String key:keyList){
	            signSb.append("&" + key + "=" +map.get(key));
	        }
	        signSb.append("&" + appSecret);
	        String signStr = signSb.toString();
	        String signKey = "";

	        try{
	            MessageDigest messageDigest = MessageDigest.getInstance("MD5");
	            String signStrEncode = Base64.getEncoder().encodeToString(signStr.getBytes());
	            messageDigest.update(signStrEncode.getBytes());
	             signKey = new BigInteger(1,messageDigest.digest()).toString(16);
	            if(signKey.length() < 32) {
	                for (int i = 0; i < (32 - signKey.length()); i++) {
	                    signKey = "0" + signKey;
	                }
	            }
	        }catch (Exception e){

	        }
	        return  signKey;

	    }
	}

打成java包
------------
	在文件路劲下执行面的命令：
	.. code-block:: shell

		javac ArtistMD5.java
		jar    cvf    ArtistMD5.jar    ArtistMD5.class

jar包引入到jmeter
-----------------
	将生成的jar包放到%JMETER_HOME%\\lib目录下




