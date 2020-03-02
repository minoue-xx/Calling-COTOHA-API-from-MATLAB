# �͂��߂�
  


����́u���������� MATLAB ���[�U�[���� Qiita �U�Ԃ�v�쐬�L�ł��B




�ŋ� MATLAB �^�O�̂����L���������Ă��Ă���悤�Ɏv���܂��̂ŁAQiita API ���g���ďW�v���Ă݂܂��B�����đO��i[�yCOTOHA API x MATLAB�zQiita ���e�L���̗v��](https://qiita.com/eigs/items/39196afdb5f28bf3ba0f)�j�Ɉ������� COTOHA API �i�ڍׁF[COTOHA API Portal](https://api.ce-cotoha.com/contents/index.html)�j�̗v��@�\���g���ď����V��ł݂܂��傤�B


  
## ���s��

   -  MATLAB R2019b 
   -  Text Analytics Toolbox 

## ���������

   -  Qiita API �� `matlab` �� `simulink` �̃^�O���t�����L���𒊏o 
   -  �����ˏ��ɕ��ׂ� COTOHA API �ŗv��쐬 
   -  2018 �N �܂Ƃ߁F[�Z���� MATLAB ���[�U�[���� Qiita �ӂ�Ԃ�i2019�N�Łj](https://qiita.com/eigs/private/34c623399298d54453ce) 
   -  2019 �N �܂Ƃ߁F[�Z���� MATLAB ���[�U�[���� Qiita �ӂ�Ԃ�i2018�N�Łj](https://qiita.com/eigs/private/a75f816a9ad2b75466b6) 



`timetable` �^�̃f�[�^�� `retime` �֐��ŏW�v����Ƃ���A�����č\���̃x�N�g���̓������Z���z��x�N�g���i�I�H�j�̏����Ȃǂ��A�}�j�A�b�N�Ō��ǂ���ł��B�܂��A�� 5000 �����𒴂��镶�͂ɂ��Ă� COTOHA API ����G���[���Ԃ��Ă���������̂ŁA���̕ӂ�������ł��؂��Ă��܂��̂ł��������������B


# Qiita API �� MATLAB/Simulink �̋L���擾


������ƂɎ��|����܂��B


```matlab
clear
loadFlag = true;

if loadFlag % �ǂݍ��܂Ȃ��ꍇ�͎��O�ǂݍ��ݍς݂̃f�[�^�� mat �t�@�C������ǂݍ��݂܂�
    % �A�N�Z�X�g�[�N���g�p�i������ token �ɏ��������Ă��������j
%     accessToken = 'Bearer xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';
%     opts = weboptions('HeaderFields',{'Authorization',accessToken});
    opts = weboptions; % �������������炱�ꂾ���ł�OK
    
    % �S������Ă� 600 �L���Ȃ̂œ��ɍ׍H�͕K�v�Ȃ������B
    page = 1;
    data = [];
    tags = ["matlab","simulink"];
    for tagid=1:2
        page = 1;
        while true
            url = "https://qiita.com/api/v2/tags/" + tags(tagid) + "/items?page="+page+"&per_page=100";
            tmp = webread(url,opts);
            if isempty(tmp)
                break;
            end
            data = [data;tmp]; %#ok<AGROW>
            page = page + 1;
        end
    end
    
    % �\���̂œ�����̂� table �^�ɕϊ�
    data = struct2table(data);
    
    % �ꉞ�d���������������`�F�b�N
    [~,ia,~] = unique(data.id);
    data = data(ia,:);
    save('allArticles.mat','data')
else
    load allArticles.mat %#ok<UNRCH>
end
```
  


���Ȃ݂ɂ��̎��_�ŕϐ��� 18 �B


```matlab
data.Properties.VariableNames'
```
```
ans = 16x1 �� cell �z��    
'rendered_body'      
'body'               
'coediting'          
'comments_count'     
'created_at'         
'group'              
'id'                 
'likes_count'        
'private'            
'reactions_count'    

```


�Ƃ肠�����A���e���A�L���̃^�C�g���A�L���̓��e�A���[�U�[���A�����ː��A�^�O�ڍׁAURL �������c���Ă����܂��B


```matlab
data = data(:,{'created_at', 'title','rendered_body','user','likes_count','tags','url'});
head(data)
```
| |created_at|title|rendered_body|user|likes_count|tags|url|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|'2018-05-05T23:01:26+09:00'|'���n��f�[�^���͂̏��Ђ̃T���v���f�[�^��MATLAB�Ŏ����Ă݂�'|



����Ȋ����B


# timetable �^�ɕϊ��ȂǁA���܂��܂����Ƃ���


���e������ 2020-02-08T19:10:45+09:00 �Ƃ����悤�ȃt�H�[�}�b�g�Ȃ̂ŁA����ɍ��킹�� `datetime` �^�ɕϊ��A������ `timetable` �^�ɕϊ����Ă����܂��B


```matlab
created_at = datetime(vertcat(data.created_at),...
    'InputFormat', "uuuu-MM-dd'T'HH:mm:ss'+09:00");
tData = table2timetable(data,'RowTimes', created_at);
```


������֌W�͂��ׂ� string �^�ɂ��Ă����܂��B���[�U�[���ɂ��Ă͑��ɂ���R��񂪋l�܂����\���̂ɂȂ��Ă���̂ł����A�����ł� id ���������o���Ă����܂��B


## url (������ in �Z���z��j


����͊ȒP


```matlab
tData.url = string(tData.url);
```


tData.url �� cell �z��ɂȂ��Ă���̂ŁA���̂܂� string �^�ɃT�N�b�ƕύX����܂��Btitle �� rendered_body �����l�ł��B


```matlab
tData.title = string(tData.title);
tData.rendered_body = string(tData.rendered_body);
```
## user (�\���́j


�\���̂͂�����Ɩʓ|�B�~�����̂� user �̒��� id �Ƃ��������o�[�����B�`�������̂����Ă݂��


```matlab
tData.user(1:2).id
```
```
ans = 'Alberobellojiro'
ans = 'nHounoki'
```


�Ƃ����u�R���}��؂胊�X�g�v�ɂȂ�܂��B




����́A�����T�C�Y�̃f�[�^�ł���� `[]` (`vertcat` or `horzcat`) �Ńx�N�g�����A�������� `{}` �ň͂߂� cell �z��Ƃ��ď����ł��܂��B�����Ƃǂ����Ă��ƂȂ��̂ł����A���\��舵���ɍ������L������݂�����܂��ˁB




�����ł� id �͂����Ȓ����̕�����̂悤�Ȃ̂ŁAcell �z��ɕϊ�������� `string` �ɂ����Ă݂܂��B


```matlab
tmp = {tData.user.id}';
tmp(1:2)
```
```
ans = 2x1 �� cell �z��    
'Alberobellojiro'    
'nHounoki'           

```
```matlab
tData.user = string(tmp);
```
## tag (�\����s in �Z���z��j


����͂܂������ʓ|�������B�Z���z��̒��ɍ\���̂��i�����j�����Ă��܂��B�Ⴆ��


```matlab
tData.tags{1}
```
|�t�B�[���h|name|versions|
|:--:|:--:|:--:|
|1|'R'|[ ]|
|2|'matlab'|[ ]|



����Ȋ����B�~�����̂� name �����Ȃ�ł����A


```matlab
{tData.tags{1}.name}
```
```
ans = 1x2 �� cell �z��    
'R'          'matlab'     

```


�Ƃ�������S�s��C�ɏ�������ɂ͎g�������ɂȂ��E�E�̂ł����͌������߂� cellfun �ōs���Ă݂܂��B


```matlab
tmp = tData.tags; % cell �z��
cellfun(@(x) string({x.name}), tmp);
```
```
�G���[: cellfun
Uniform �̏o�͂̃C���f�b�N�X 1 �ɂ���o�� 1 ���X�J���[�ł���܂���B
'UniformOutput' �� false �ɐݒ肵�Ă��������B
```


���ꂼ��̃Z���z��̒��g�̍\���̂��� name �t�B�[���h����Ă��āA��������Z���z��ɂ������ string ������A�Ƃ����������Ă����ł����AUniformOutput ����Ȃ��Ɠ{���܂��B�v�͋L�����Ƃ� tag �̐����Ⴄ�̂ŁA�A���ł��܂���Ƃ����Ӗ��ł��B���炻�����B




�����̓G���[���b�Z�[�W�ɏ]���ăI�v�V������t���āA�Z���z��Ƃ��ďo�͂��Ă����܂��B


```matlab
tData.tags = cellfun(@(x) string({x.name}), tmp, 'UniformOutput', false);
tData.tags(1:2)
```
| |1|
|:--:|:--:|
|1|1x2 string|
|2|1x3 string|

```matlab
tData.tags{1}
```
```
ans = 1x2 �� string �z��    
"R"          "matlab"     

```


����Ȋ����B


  
# ���ԓ��e������


�����ł悤�₭�Ђƒi���E�E�B




�Z�����\���̂��\���̂̃x�N�g�����ʓ|�ł������A�ЂƂ܂��܂Ƃ܂����̂Ō��ԓ��e���̐��ڂł����Ă݂܂��B�����͌l�I�ɂ��C�ɓ���́i����񂪂ȁj `retime` �֐��̏o�Ԃł��B


```matlab
tmp = retime(tData(:,'title'),'monthly','count');
bar(tmp.Time,tmp.title)
title('# of post with MATLAB/Simulink tag')
ylabel('# of post')
grid on
```

![figure_0.png](Example_QiitaSummarization_images/figure_0.png)



Qiita �S�̂̊������Ɉ��������Ă� MATLAB �֘A�L�����e���������ÂL�тĂ��Ă��܂����A��N�㔼�ɑ傫���L�тĂ��܂��ˁB


## ���Ԃ����ˑ���


���łɁB���x�͋L���̃J�E���g�ł͂Ȃ��A�����˂̑����Ȃ̂� `'count`' �� `'sum'` �ɕς��Ă����܂��B


```matlab
tmp = retime(tData(:,"likes_count"),'monthly','sum');
bar(tmp.Time,tmp.likes_count)
title('# of likes with MATLAB/Simulink tag')
ylabel('# of likes')
grid on
```

![figure_1.png](Example_QiitaSummarization_images/figure_1.png)



2015 �N�ɑ傫�Ȉُ�l�i�H�j������܂��ˁB2019 �N�㔼���������Ă����ł����A����������Ă��܂��Ă��܂��ˁE�E�B5000 �z���͂������B




���̋L���ł��F[���w������Ă����Љ�l�v���O���}���@�B�w�K�̕׋����n�߂�ۂ̍ŒZ�o�H](https://qiita.com/daxanya1/items/218f2e3b922142550ef9)


  


`'monthly'` �̂Ƃ���� `'yearly'` �ɂ���ΔN�ԁA`'weekly'` �ɂ���ΏT�ԁA`'secondly'` �ɂ���Ζ��b���Ƃ̏W�v������D����́B���ɂ��g���ǂ��날��Ǝv���̂ŁA�ڍׂ�[ retime �֐��̃w���v�y�[�W](https://jp.mathworks.com/help/matlab/ref/timetable.retime.html)�����Ă�������


  
# ���Ė{��̗v��


2018�N�A2019�N�ɓ��e���ꂽ�L���̂����˃g�b�v50�ɂ��� 2 ���ŗv�񂵂Ă��炢�܂��B




COTOHA API ���g�������͑O��i[�yCOTOHA API x MATLAB�zQiita ���e�L���̗v��](https://qiita.com/eigs/items/39196afdb5f28bf3ba0f)�j�Ɠ����ł����A�L���̒����� 5000 �����𒴂���ƃG���[���o�錻�ۂɌ�����ꂽ�̂ŁA5000�����𒴂�����L���ɂ��ẮA��������O����2500�����A�㔼��2500�������g���܂��B


## **�A�N�Z�X�g�[�N�����擾����**


`clientid` �� `clientsecret` �͓K�X���������Ă��������B


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
## 2019�N�܂Ƃ߁i�����ˏ��j


2019 �N�̋L�������o���āA�����ˏ��ɕ��בւ��ďォ��50�L���ɂ��ėv������Ă��炢�܂��B


```matlab
trange = timerange(datetime(2019,1,1),datetime(2020,1,1));
tData2019 = tData(trange,:);
tData2019 = sortrows(tData2019,'likes_count','descend');
```


COTOHA �� �Q ���ɗv��B


```matlab
COTOHAsummary = strings(height(tData2019),1);
for ii=1:50
    COTOHAsummary(ii) = getSummary(tData2019.rendered_body(ii),tokens,2);
end
tData2019.COTOHAsummary = COTOHAsummary;
```


Markdown �ŏ����o���Č�� Qiita �ɃR�s�y�B


```matlab
md = generateMarkdown(tData2019, "# 2019 �܂Ƃ�");

mdfile = "Qiita2019" + ".md";
fileID = fopen(mdfile,'w');
fprintf(fileID,'%s\n',md);
fclose(fileID);

```
## 2018�N�܂Ƃ߁i�����ˏ��j


2018 �N�̋L�������o���āA�����ˏ��ɕ��בւ��ďォ��50�L���ɂ��ėv������Ă��炢�܂��B


```matlab
trange = timerange(datetime(2018,1,1),datetime(2019,1,1));
tData2018 = tData(trange,:);
tData2018 = sortrows(tData2018,'likes_count','descend');
```


COTOHA �� 2 ���ɗv��B


```matlab
COTOHAsummary = strings(height(tData2018),1);
for ii=1:50
    COTOHAsummary(ii) = getSummary(tData2018.rendered_body(ii),tokens,2);
end
tData2018.COTOHAsummary = COTOHAsummary;
```


Markdown �ŏ����o���Č�� Qiita �ɃR�s�y�B


```matlab
md = generateMarkdown(tData2018, "# 2018 �܂Ƃ�");

mdfile = "Qiita2018" + ".md";
fileID = fopen(mdfile,'w');
fprintf(fileID,'%s\n',md);
fclose(fileID);
```
# �܂Ƃ�


Qiita API �ł̓����_�����O���ꂽ�L���Ƃ͕ʂ� 'body' �ŁAmarkdown �o�[�W���������o���܂����A�������o��Ƃɂ� html �̕����y�ł����B




�����E�R�[�h�����͂��������菜���ď��������܂������A�^�C�g���{�v��ł�����x���g���z�������܂��ˁB��ʂ̋L������������c�����ēǂނ��̂�I�ԂƂ����p�r�ɂ͂悳�����ȋC�����Ă��܂����B


  


[�Z���� MATLAB ���[�U�[���� Qiita �ӂ�Ԃ�i2018�N�Łj](https://qiita.com/eigs/private/34c623399298d54453ce)




[�Z���� MATLAB ���[�U�[���� Qiita �ӂ�Ԃ�i2019�N�Łj](https://qiita.com/eigs/private/a75f816a9ad2b75466b6)


  


COTOHA API �������Ă݂����I�Ƃ������̂����ɗ��Ă���������ł��B


# Appendix
## getSummary �֐�
```matlab
function summary = getSummary(htmlSource, tokens, sent_len)

tree = htmlTree(htmlSource);

selector = "h1,h2,h3,p,li";
subtrees = findElement(tree,selector);

% check if details contained in p
index = false(length(subtrees),1);
for ii=1:length(subtrees)
    tmp = findElement(subtrees(ii),'details');
    index(ii) = isempty(tmp); % <DETAILS> ������� false �ɂȂ�
end

% DETAILS ������ P, LI ����
subtreesNoDetails = subtrees(index);

% ���͕�
sentence = extractHTMLText(subtreesNoDetails);

sentence = join(sentence);
if strlength(sentence) > 5000
    tmp = char(sentence);
    sentence = string(tmp([1:2500,end-2499:end]));
end
strlength(sentence);

% Call COTOHA API
baseurl = 'https://api.ce-cotoha.com/api/dev/';
accesstoken = tokens.access_token;
Header = {'Content-Type', 'application/json;charset=UTF-8'; 'Authorization', ['Bearer ' accesstoken]};
Body = struct('document', sentence, ...
    'sent_len', num2str(sent_len));
options = weboptions('RequestMethod','post', 'MediaType','application/json','HeaderFields', Header);

response = webwrite([baseurl 'nlp/beta/summary'], Body, options);
summary = string(response.result);

end
```
## generateMarkdown �֐�
```matlab
function md = generateMarkdown(tData, header)

md = header + newline + newline;
for ii=1:50
    title = tData.title(ii);
    url = tData.url(ii);
    md = md + "## " + ii + ": [" + title + "]("+url+")" + newline;
    likes = tData.likes_count(ii);
    user = tData.user(ii);
    date = tData.Time(ii);
    date.Format = 'yyyy/MM/dd';
    
    md = md + "@" + user + " ���� (" ...
        + string(date) + " ���e)" + ": **" + string(likes) + "**" + " ������" ...
        + newline;
    
    tags = tData.tags{ii};
    tags = "```" + tags + "```";
    md = md + "**Tags** :" + join(tags) + newline;
    
    summary = tData.COTOHAsummary(ii);
    if strlength(summary) > 150 % �����v��͑ł��؂����Ⴂ�܂��B
        tmp = char(summary);
        summary = string(tmp(1:150)) + "...(����)";
    end
    md = md + newline + ...
        "> " + summary + newline + newline;
    
end

end
```
