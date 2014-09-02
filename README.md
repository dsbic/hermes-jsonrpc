hermes-jsonrpc [![Build Status](https://travis-ci.org/knightliao/hermes-jsonrpc.svg?branch=master)](https://travis-ci.org/knightliao/hermes-jsonrpc) [![Coverage Status](https://coveralls.io/repos/knightliao/hermes-jsonrpc/badge.png)](https://coveralls.io/r/knightliao/hermes-jsonrpc)
==============

A Java-Version light-weight HTTP-JSON RPC framework using GSON/Protostuff.

使用 GSON/Protostuff 的轻量级HTTP协议的Java Json Rpc框架

hermes-jsonrpc当前最新版本：

- dev:    1.0.2-SNAPSHOT
- stable：1.0.1

在Maven Central Repository里查看 [com.github.knightliao.hermesjsonrpc](http://search.maven.org/#search%7Cga%7C1%7Ccom.github.knightliao.hermesjsonrpc )


## 项目信息 ##

- Java项目(1.6+)
- Maven管理(3.0.5+)

## 它是什么? ##

- 命名为hermes-jsonrpc
- 专注于高效、高速、简单的 Java Json Rpc 编程

## Features ##

- 协议：HTTP
- 传输格式：JSON
- codec协议: GSON 或 Protostuff
- Client编程方式：
	- 支持Spring AOP代理方式请求方式
- Server编程方式：
	- 支持Spring Web Servlet接受请求方式
	- 支持安全的 用户名/密码验证(无法反算)
	- 支持白名单
	- 支持接受GET请求，它显示接口信息。GET请求支持白名单
- 同步调用，不支持异步调用

注：本框架遵循的规范可参见: [https://github.com/knightliao/docs/blob/master/baidu/rpc/rpcspec.md](https://github.com/knightliao/docs/blob/master/baidu/rpc/rpcspec.md)

## 协议规范示例 ##

###Java接口:####

	package com.github.knightliao.hermesjsonrpc.demo;
	
	/**
	 * 
	 * @author liaoqiqi
	 * @version 2014-8-21
	 */
	public interface DemoServiceDriver {
	
	    public class Request {
	
	        public Request(int maxValue, int minValue) {
	            super();
	            this.maxValue = maxValue;
	            this.minValue = minValue;
	        }
	
	        private int maxValue;
	
	        public int getMaxValue() {
	            return maxValue;
	        }
	
	        public void setMaxValue(int maxValue) {
	            this.maxValue = maxValue;
	        }
	
	        public int getMinValue() {
	            return minValue;
	        }
	
	        public void setMinValue(int minValue) {
	            this.minValue = minValue;
	        }
	
	        private int minValue;
	    }
	
	    public class Response {
	
	        public Response(int value) {
	            super();
	            this.value = value;
	        }
	
	        private int value;
	
	        public int getValue() {
	            return value;
	        }
	
	        public void setValue(int value) {
	            this.value = value;
	        }
	    }
	
	    Response getRandom(Request seed);
	}

###client request: ###

	{"method":"getRandom","version":"2.0","params":[{"maxValue":0,"minValue":50}],"id":39547}

###server response:###
	
	{"result":{"value":27},"version":"2.0","id":39547}

## 使用 ##

在您的 Maven POM 文件里加入：

client:

    <dependency>
        <groupId>com.github.knightliao.hermesjsonrpc</groupId>
        <artifactId>hermes-jsonrpc-client</artifactId>
        <version>1.0.1</version>
    </dependency>

server:

    <dependency>
        <groupId>com.github.knightliao.hermesjsonrpc</groupId>
        <artifactId>hermes-jsonrpc-server</artifactId>
        <version>1.0.1</version>
    </dependency>

主要依赖为：

- apollo(1.0.1)

### Tutorials ###

- [Tutorial 1 Json GSON RPC Server撰写方法（最佳实践）](https://github.com/knightliao/hermes-jsonrpc/wiki/Tutorial1)
- [Tutorial 2 Json GSON RPC Client 撰写方法（最佳实践）](https://github.com/knightliao/hermes-jsonrpc/wiki/Tutorial2)
- [Tutorial 3 带有权限验证和IP白名单的 Json GSON RPC Server撰写方法（最佳实践）](https://github.com/knightliao/hermes-jsonrpc/wiki/Tutorial3)
- [Tutorial 4 请求带有权限验证 Json GSON RPC Client 撰写方法（最佳实践）](https://github.com/knightliao/hermes-jsonrpc/wiki/Tutorial4)
- [Tutorial 5 Json Protostuff RPC 撰写方法（最佳实践）](https://github.com/knightliao/hermes-jsonrpc/wiki/Tutorial5)
	
## 局限性 ##

- 服务和客户端均只能是Java语言编程
- 不支持异步调用 
