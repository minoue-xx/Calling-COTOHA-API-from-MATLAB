# What is COTOHA API?


COTOHA API developed by NTT group provides natural language processing specialised in Japanese. See [https://api.ce-cotoha.com/contents/index.html](https://api.ce-cotoha.com/contents/index.html)




COTOHA API is capable of various tasks (see [https://api.ce-cotoha.com/contents/api-all.html](https://api.ce-cotoha.com/contents/api-all.html) for details) and some advanced capabilities are



   -  Parsing  
   -  Reference Resolution 
   -  Keyword Extraction 
   -  Speech Recognition 
   -  Speech Synthesis 
   -  Summarization 



I believe these capabilities to be fully functional, texts still need some preprocessing where MATLAB and Text Analytics Toolbox come in handy.


  
# Calling COTOHA API from MATLAB
## Step 0. Getting security tokens


Users need to use their own `clientid` and `clientsecret`.


```matlab
clientid = 'input_your_Client_ID';
clientsecret = 'input_your_Client_secret';

url = 'https://api.ce-cotoha.com/v1/oauth/accesstokens';
options = weboptions('RequestMethod','post', 'MediaType','application/json');
Body = struct('grantType', 'client_credentials', ... 
          'clientId', clientid, ...
          'clientSecret', clientsecret);
tokens = webwrite(url, Body, options);
```
## Step 1-1. Summarize documents


COTOHA API [Reference](https://api.ce-cotoha.com/contents/reference/apireference.html) provides the following example code


> curl -X POST -H 'Content-Type:application/json;charset=UTF-8' -H 'Authorization:Bearer [Access Token]' -d '{"document":"�O���������m��ɒ�؂��Ă��܂��B����A���C�����瓇�ߊC�ɂ����āA�k���{���瓌���{�����₩�ɕ����Ă��܂��B�֓��n���́A���ꎞ�X�܂�A�Ƃ���ɂ��J�ƂȂ��Ă��܂��B�����́A��������C��O���̉e���ɂ��A�����܂�ŁA��͉J�ƂȂ�ł��傤�B","sent_len":"1"}' [API Base URL]/nlp/beta/summary




In MATLAB this task can be done by the following code


```matlab
documents = "�O���������m��ɒ�؂��Ă��܂��B����A���C�����瓇�ߊC�ɂ����āA" ...
    + "�k���{���瓌���{�����₩�ɕ����Ă��܂��B�֓��n���́A���ꎞ�X�܂�A�Ƃ���ɂ��J" ...
    + "�ƂȂ��Ă��܂��B�����́A��������C��O���̉e���ɂ��A�����܂�ŁA��͉J�ƂȂ�ł��傤�B";

baseurl = 'https://api.ce-cotoha.com/api/dev/';
accesstoken = tokens.access_token;

Header = {'Content-Type', 'application/json;charset=UTF-8';
    'Authorization', ['Bearer ' accesstoken]};
Body = struct('document', documents, ... 
          'sent_len', '1');
options = weboptions('RequestMethod','post', ...
    'MediaType','application/json','HeaderFields', Header);

response = webwrite([baseurl 'nlp/beta/summary'], Body, options)
```
```
response = 
    result: '�����́A��������C��O���̉e���ɂ��A�����܂�ŁA��͉J�ƂȂ�ł��傤�B'
    status: 0

```


The response contains a summary sentense of the provided documents. Other functionalities of COTOHA API can be called similarly.


