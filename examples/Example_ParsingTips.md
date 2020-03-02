# �`�ԑf���
  
# �͂��߂�


COTOHA API ���g�����ʔ������e���łĂ��܂��ˁB����ȊF����̋L�����y���݂Ȃ���n���ɗV��ł���킯�ł����A����͊�{�ɗ����߂��č\����́i�`�ԑf��́j���m�F���Ă݂܂��B�v�_�͈ȉ��̂R�_�ł�


  

   -  *�|�C���g�P�F���R�������舵���ۂɎg�p���鎫���͏d�v* 
   -  *�|�C���g�Q�F*�����̒ǉ����@ 
   -  *�|�C���g�R*�FCOTOHA API �ɂ��\��*����* 



![image_0.png](Example_ParsingTips_images/image_0.png)


## ��

   -  MATLAB R2019b 
   -  Text Analytics Toolbox 
   -  COTOHA API v1 

  
# �`�ԑf��͂��āH
  
> **�`�ԑf���**�i�������������������A*Morphological Analysis*�j�Ƃ́A���@�I�ȏ��̒��L�̖���[���R����](https://ja.wikipedia.org/wiki/%E8%87%AA%E7%84%B6%E8%A8%80%E8%AA%9E)�̃e�L�X�g�f�[�^�i[��](https://ja.wikipedia.org/wiki/%E6%96%87)�j����A�Ώی����[���@](https://ja.wikipedia.org/wiki/%E6%96%87%E6%B3%95)��A**����**�ƌĂ΂��[�P��](https://ja.wikipedia.org/wiki/%E8%AA%9E)�̕i�����̏��ɂ��ƂÂ��A[�`�ԑf](https://ja.wikipedia.org/wiki/%E5%BD%A2%E6%85%8B%E7%B4%A0)�i*Morpheme*, �����܂��ɂ����΁A[����](https://ja.wikipedia.org/wiki/%E8%A8%80%E8%AA%9E)�ňӖ������ŏ��P�ʁj�̗�ɕ������A���ꂼ��̌`�ԑf��[�i��](https://ja.wikipedia.org/wiki/%E5%93%81%E8%A9%9E)���𔻕ʂ����Ƃł���B�i[Wikipedia](https://ja.wikipedia.org/wiki/%E5%BD%A2%E6%85%8B%E7%B4%A0%E8%A7%A3%E6%9E%90)�j


  


�Ƃ������ƂŎ��R���ꏈ���ł͌������Ȃ���Ƃ̂悤�ł��B�Ⴆ�� MATLAB �ł� [MeCab](https://ja.wikipedia.org/wiki/MeCab) ���g�p����Ă���A`tokenizedDocument` �֐��Ŏ��s���܂��B


```matlab
str = "���n��f�[�^�ɋ@�B�w�K���������B";
documents = tokenizedDocument(str);
tokenDetails(documents)
```
| |Token|DocumentNumber|LineNumber|Type|Language|PartOfSpeech|Lemma|Entity|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|"��"|1|1|letters|ja|noun|"��"|non-entity|
|2|"�n��"|1|1|letters|ja|noun|"�n��"|non-entity|
|3|"�f�[�^"|1|1|letters|ja|noun|"�f�[�^"|non-entity|
|4|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|5|"�@�B"|1|1|letters|ja|noun|"�@�B"|non-entity|
|6|"�w�K"|1|1|letters|ja|noun|"�w�K"|non-entity|
|7|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|8|"����"|1|1|letters|ja|verb|"����"|non-entity|
|9|"��"|1|1|letters|ja|auxiliary-verb|"��"|non-entity|
|10|"�B"|1|1|punctuation|ja|punctuation|"�B"|non-entity|



����ȋ�ł��B


  
## �u���n��f�[�^�v=>�u���v�u�n��v�u�f�[�^�v


 �u���n��v���u���v�u�n��v�ɁA�u�@�B�w�K�v���u�@�B�v�u�w�K�v�ƕ�������Ă���̂��C�ɂȂ�܂��B����� MeCab �Ŏg�p���鎫���i����F IPADIC�j�ɂ��̒P�ꂪ�����Ă��Ȃ����Ƃ��v�����Ɛ������܂����A���������`�ԑf��͂Ƃ͍�������ʂɔF������p�r�ł͂Ȃ��̂�������Ȃ��B




���̕ӂ���������Ă��܂����`�ԑf�����̂܂܎g���ƁA���͂̃g�s�b�N���͂�L�[���[�h���o�ɉe����^���邱�ƂɂȂ肻���ł��B�Z�p�֌W�̒P�ꂪ�����A�Ⴆ�� Qiita �̓��e�L���𕪐͂��悤�Ƃ���Ƃ�����ƐS�z�B




�Ⴆ�΂��̗�F[Word-By-Word Text Generation Using Deep Learning](https://jp.mathworks.com/help/textanalytics/ug/word-by-word-text-generation-using-deep-learning.html) �ł� LSTM ���g���āi�p��j���͐������Ă��܂��B�������@�����̂܂܍ׂ�����������Ă��܂������{��Ɏg���Ɖp����̌��ʂ��o�Ȃ��C�����܂��ˁB[�`�ԑf��͂����ĒP������o���Ă������E�E�E���H](https://qiita.com/icoxfog417/items/e83383263badec7a4805) by @icoxfog417 �ł���������Ă���悤�ȁu�`�ԑf��́v�Ɓu�P��v���ƁA�u�P��v���g�p���ׂ��ł��傤�B




*����ȕ�����ɂ��Ắu*[�`�ԑf��͂ł̌����I�ȕ����ꏈ��](https://ci.nii.ac.jp/naid/110002911631)�i�ؘa�v �� - ��2003�j*�v�Ȃǂ����Ȃ��b������܂��B*


  
# COTOHA API �ł́H


����Ă݂܂��B���Ȃ݂� COTOHA API �񋟂���u�\����� API �v�ł͌`�ԑf�ɕ������邾���łȂ��A���ߊԂ̌W��󂯊֌W��`�ԑf�Ԃ̌W��󂯊֌W�܂ŏo���Ă���܂��B


  
### �A�N�Z�X�g�[�N���ݒ�


`clientid` �� `clientsecret` �͂����g�̂��̂��w�肭�������B


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
### �\����� API


�Ăяo���܂��B


```matlab
baseurl = 'https://api.ce-cotoha.com/api/dev/';
accesstoken = tokens.access_token;
Header = {'Content-Type', 'application/json;charset=UTF-8'; 'Authorization', ['Bearer ' accesstoken]};
Body = struct('sentence', "���n��f�[�^�ɋ@�B�w�K���������B", ...
    'type', 'default');

options = weboptions('RequestMethod','post', 'MediaType','application/json','HeaderFields', Header);
response = webwrite([baseurl 'nlp/v1/parse'], Body, options);
```
  
### �g�[�N���������o


���ʂ͓���g�񂾍\���̂ŕԂ��Ă��Ă����ȏ�񂪓����Ă��܂��i�ڍׁF[�\����� API](https://api.ce-cotoha.com/contents/reference/apireference.html#parsing_io_meaning)�j�B���̒m���ł͂��ׂĂ��g�����Ȃ��Ȃ��̂ŁA�����ł͕\�L�iform�j�Ƃ��̒P��̏o�����A�����ĕ��߁ichunk�j�̏������o���܂��B�֐�����Ă����܂����i�y�[�W�����j�̂ŋ����̂�����͌��Ă��������B


```matlab
[listofToken, chunkList] = getTokens(response);
listofToken
```
| |chunkIDs|IDs|forms|
|:--:|:--:|:--:|:--:|
|1|1|0|"���n��"|
|2|1|1|"�f�[�^"|
|3|1|2|"��"|
|4|2|3|"�@�B"|
|5|2|4|"�w�K"|
|6|2|5|"��"|
|7|3|6|"��"|
|8|3|7|"��"|
|9|3|8|"��"|
|10|3|9|"�B"|



����ȋ�B�@�B�w�K�́u�@�B�v�Ɓu�w�K�v�ł����A�u���n��v�͔F������Ă���݂����ł��B




COTOHA API �� Enterprise ���[�U�݂̂ł����A��͂Ɏg�p������p�ꎫ�����ʓr�w��\�B11��ނ�����̂œ���̕���ɓ����������͂̏ꍇ�͎g��Ȃ���͂Ȃ������ł��ˁB


  
### ���ߊԂ̌W��󂯊֌W


���łɕ��̂Ȃ�������Ă݂܂��B`digraph` �֐����g���ėL���O���t�ŕ\�����܂��B




�e���߂� 1 �̃m�[�h�ƍl���邱�Ƃɂ��āA�e���߂ɑ�����P�ꓯ�m�� `join` �֐��Ōq����Ċe�m�[�h�̃��x���Ƃ��܂��B


```matlab
nodelabels = splitapply(@(x) join(x,""),listofToken.forms,listofToken.chunkIDs); % ���� chunkID �� forms �͌���
g = digraph(chunkList,nodelabels,'omitselfloops');
plot(g,'Layout','layered','NodeFontSize',12);
```

![figure_0.png](Example_ParsingTips_images/figure_0.png)



�\���������܂����B����͗V�т��������肻���Ȃ̂ő��̗���y�[�W�����ŏЉ�܂��B


# �g�����v���F�ŗL����


�����P�B


```matlab
str = "�h�i���h�E�g�����v���}�N�h�i���h�Ńg�����v��";
Body = struct('sentence',str, 'type', 'default');
response = webwrite([baseurl 'nlp/v1/parse'], Body, options);
getTokens(response)
```
| |chunkIDs|IDs|forms|
|:--:|:--:|:--:|:--:|
|1|1|0|"�h�i���h�E�g�����v"|
|2|1|1|"��"|
|3|2|2|"�}�N�h�i���h"|
|4|2|3|"��"|
|5|3|4|"�g�����v"|
|6|3|5|"��"|



COTOHA API �̓g�����v�����F�����Ă܂��ˁB���Ȃ݂� MeCab �ƃf�t�H���g�̎����iIPADIC�j���g����


```matlab
documents = tokenizedDocument(str);
tokenDetails(documents)
```
| |Token|DocumentNumber|LineNumber|Type|Language|PartOfSpeech|Lemma|Entity|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|"�h�i���h"|1|1|letters|ja|proper-noun|"�h�i���h"|person|
|2|"�E"|1|1|punctuation|ja|symbol|"�E"|non-entity|
|3|"�g�����v"|1|1|letters|ja|noun|"�g�����v"|non-entity|
|4|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|5|"�}�N�h�i���h"|1|1|letters|ja|proper-noun|"�}�N�h�i���h"|organization|
|6|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|7|"�g�����v"|1|1|letters|ja|noun|"�g�����v"|non-entity|
|8|"��"|1|1|letters|ja|adposition|"��"|non-entity|



���ꂾ�Ɓi�h�i���h�E�j�g�����v�ƃg�����v���������ɂȂ�������Ă��܂��B




����͂킴�Ƃ炵����ł����A���̕ӂ̑O�������ŏI���ʂɗ^����e���͑傫���̂ŁA�O�����͂߂�ǂ������炸�ɂ����������ƃC�P�i�C�Ƃ������P�ł��ˁB


# �΍�P�FCustomTokens �I�v�V����


������Ƃ��đΉ����K�v�ȗp�ꂪ�����łł���� `CustomTokens` �I�v�V�������g���������܂��B


```matlab
documents = tokenizedDocument(str,"CustomTokens","�h�i���h�E�g�����v");
tokenDetails(documents)
```
| |Token|DocumentNumber|LineNumber|Type|Language|PartOfSpeech|Lemma|Entity|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|"�h�i���h�E�g�����v"|1|1|custom|ja|other|"�h�i���h�E�g�����v"|non-entity|
|2|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|3|"�}�N�h�i���h"|1|1|letters|ja|proper-noun|"�}�N�h�i���h"|organization|
|4|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|5|"�g�����v"|1|1|letters|ja|noun|"�g�����v"|non-entity|
|6|"��"|1|1|letters|ja|adposition|"��"|non-entity|



�s���ȒP��Ƃ��ĔF�����ꂿ�Ⴂ�܂����A���Ȃ��Ƃ��g�����v�Ƃ̌�F���͔������܂��B


# �΍�Q�F�����̒ǉ�


���������̓��ʑΉ��ł���Ώ�ł̕��@�ł�����������܂��񂪁A��R����ꍇ�ɂ̓f�t�H���g�Ŏg�p����  IPADIC �ɉ����� IPADIC �ɒǉ��̎�����^���Ă������悳�����ł��B 




�I�����͂Q�F



   1.  �����łP������F��ς����ǃj�b�`�ȕ���̕��͂��Ώۂł���΂��傤���Ȃ��E�E�B 
   1.  ���J����Ă��鎫�����g���F�҂����荇��������������΂����񂾂��ǁB 



�Ⴆ��



   -  ��Õ���F [ComeJisyo](https://ja.osdn.net/projects/comedic/)�i�R���f�B�J�����H�p�j, [MANBYO](http://sociocom.jp/~data/2018-manbyo/index.html)�i�a����Ǐ�j 
   -  �Ȋw�Z�p�S�ʁi�H�j: [�Ȋw�Z�p�p��`�ԑf��͎���](https://dbarchive.biosciencedbc.jp/jp/mecab/desc.html) (CC �o�C�I�T�C�G���X�f�[�^�x�[�X�Z���^�[ CC BY-SA 4.0) 



�Ȃǂ�������܂����BComeJisyo �͐́A��Õ��͂̉�͂Ɏg�������Ƃ�����܂��B�Q�l�F[Ubuntu��MeCab�Ɉ�×p�ꎫ��(ComeJisyo,MANBYO)��ǉ����Ă݂�](https://qiita.com/yama_ebi/items/73ed13b43ace1a3e5606) by @yama_ebi ����


  


���Ƃ� [mecab-ipadic-NEologd](https://github.com/neologd/mecab-ipadic-neologd/blob/master/README.ja.md) �ɂ͑�ϋ������Ђ���܂����B


> mecab-ipadic-NEologd �͌`�ԑf��̓G���W�� MeCab �Ƌ��Ɏg���P�ꕪ�������������ŁA�T2��ȏ�X�V����A�V��E�ŗL�\���ɋ����A��b���������A�������I�[�v���\�[�X�E�\�t�g�E�F�A�ł��� �Ƃ�������������܂��B�i[�V��E�ŗL�\���ɋ����umecab-ipadic-NEologd�v�̌��ʂ𒲂ׂĂ݂�](https://engineering.linecorp.com/ja/blog/mecab-ipadic-neologd-new-words-and-expressions/)�j




�T2��ȏ�X�V�Ƃ��A�V��Ή��ւ̋C���̓���悤�����Ƃ͈�����悵�܂��B�ǂ��������Ă���񂾁E�E�B�����N�������ƐV��ւ̑Ή��i�e���r�ԑg���A�ŗL�����Ȃǁj�͑f���炵���͗l�ł��B


# MATLAB �Ŏg����̂��H


���ꂼ��̎g�p��͂܂��@�����ΓZ�߂����Ǝv���܂����A��{�I��


```matlab
mecabOptions
```
```
ans = 
  MecabOptions �̃v���p�e�B:

             Model: "C:\Program Files\MATLAB\R2019b\sys\share\dict-ipadic"
         UserModel: ""
    LemmaExtractor: @textanalytics.ja.mecabToLemma
      POSExtractor: @textanalytics.ja.mecabToPOS
      NERExtractor: @textanalytics.ja.mecabToNER

```


���� `UserModel` �Ɏ��� dic �t�@�C���̃p�X��ݒ肷�邾����OK�ł��B




�����ł͌��ʂ����ɂ��܂����A��ŐG�ꂽ [JST�V�\�[���X���o����E���`�ꎫ��](https://dbarchive.biosciencedbc.jp/jp/mecab/data-1.html) �i�Ȋw�Z�p�p��`�ԑf��͎����j���g���Ă݂��


```matlab
% Thesaurus2015.dic �͏�̃����N�悩��ʓr�_�E�����[�h���Ă�������
mOptions = mecabOptions('UserModel',"Thesaurus2015.dic");
str = "���n��f�[�^�ɋ@�B�w�K���������B";
documents = tokenizedDocument(str,"TokenizeMethod",mOptions);
tokenDetails(documents)
```
| |Token|DocumentNumber|LineNumber|Type|Language|PartOfSpeech|Lemma|Entity|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|"���n��"|1|1|letters|ja|noun|"���n��"|non-entity|
|2|"�f�[�^"|1|1|letters|ja|noun|"�f�[�^"|non-entity|
|3|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|4|"�@�B�w�K"|1|1|letters|ja|noun|"�@�B�w�K"|non-entity|
|5|"��"|1|1|letters|ja|adposition|"��"|non-entity|
|6|"����"|1|1|letters|ja|verb|"����"|non-entity|
|7|"��"|1|1|letters|ja|auxiliary-verb|"��"|non-entity|
|8|"�B"|1|1|punctuation|ja|punctuation|"�B"|non-entity|



����ǂ́u���n��v�Ɓu�@�B�w�K�v�����ꂼ��P��Ƃ��ĔF������Ă��܂��B����͂悳���B




���̗�̂悤�� `dic` �t�@�C�������J����Ă�����̂�����΁A�ʂ̃t�@�C���icsv ���j���� dic �t�@�C�������K�v������ꍇ������܂��B


  
# �܂Ƃ�


����͎����ƌ`�ԑf��͂̌��ʂɂ��ĐG��Ă݂܂����B�����ŉ_�ɕ��͂𕪉����ă��f���ɓ���Ă��������Ƃɂ͂Ȃ�Ȃ����B�V���ŗL�����ɋ������� [mecab-ipadic-NEologd](https://github.com/neologd/mecab-ipadic-neologd/blob/master/README.ja.md) �͖ʔ������Ȃ̂ŁA����g���Ă݂Ă܂Ƃ߂Ă݂����Ǝv���܂��B�i�ł��邩�ȁj




COTOHA API �ŗp�ӂ���Ă��鎫���̐^���� Enterprise ���[�U�[�ɂȂ�Ί��\�ł���悤�ł����A���������`�ԑf��͈ȏ�̋@�\�������R�Ȃ̂ŁA���܂�傫�Ȗ��ł͂Ȃ��ł��ˁB


  
# ���܂��F���߂̌W��󂯉���


COTOHA API �̍\����� API �̌��ʂɂ͊e�P��̈ˑ��֌W�����łȂ��A���߂̌W��󂯏����܂܂�Ă��܂��B�����ł͕��ߊԂ̂Ȃ�������Ă݂܂��傤�B


## �ƂȂ�̋q�͂悭�`�H���q��
```matlab
str = "�ƂȂ�̋q�͂悭�`�H���q��";
Body = struct('sentence', str, 'type', 'default');

options = weboptions('RequestMethod','post', 'MediaType','application/json','HeaderFields', Header);
response = webwrite([baseurl 'nlp/v1/parse'], Body, options);

% �\�L�A���ߏ��̒��o
[listofToken, chunkList] = getTokens(response);

% ���� chunkID �� forms �͌������ăm�[�h����
nodelabels = splitapply(@(x) join(x,""),listofToken.forms,listofToken.chunkIDs);  
g = digraph(chunkList,nodelabels,'omitselfloops');
plot(g,'Layout','layered','NodeFontSize',12);
```

![figure_1.png](Example_ParsingTips_images/figure_1.png)



���R����I�ɂǂꂭ�炢�Ӌ`�����邩������܂��񂪁A�ǂ̃��[�g������Ă����Ƃ��Đ������Ă��܂��ˁB



   -  �ƂȂ�̋q�͐H���q�� 
   -  �ƂȂ�̋q�͋q�� 
   -  �悭�H���q�� 
   -  �悭�`�H���q�� 

## �����Ԃ�����H�ׂ��L


�����ȉ��߂̉\�������镶�B�ڍׂ͂�����u[��������̉��߂��ł���u�����Ԃ�����H�ׂ��L�v���ʔ���](https://nihongonosensei.net/?p=7442)�v�B�e���ߕʂɊG���t���Ă���̂Ŗʔ����ł��BCOTOHA API �ł͂ǂ�ȗ����������ł��傤���E�E�B


```matlab
str = "�����Ԃ�����H�ׂ��L�B";
Body = struct('sentence', str, 'type', 'default');

options = weboptions('RequestMethod','post', 'MediaType','application/json','HeaderFields', Header);
response = webwrite([baseurl 'nlp/v1/parse'], Body, options);

% �\�L�A���ߏ��̒��o
[listofToken, chunkList] = getTokens(response);

% ���� chunkID �� forms �͌������ăm�[�h����
nodelabels = splitapply(@(x) join(x,""),listofToken.forms,listofToken.chunkIDs);
g = digraph(chunkList,nodelabels,'omitselfloops');
plot(g,'Layout','layered','NodeFontSize',12);
```

![figure_2.png](Example_ParsingTips_images/figure_2.png)


   -  �Ԃ�����H�ׂ��L 
   -  �����H�ׂ��L 
   -  ��������H�ׂ��L 



�����I�Ȃ̂́u**�����Ԃ���**��H�ׂ��L�v�ł��傤���E�E�B


> ���{��͕��߂ŏ��Ԃ����ւ�����̂ŁA�C���߂Ɣ�C���߂ɋ����������Ă����������{��Ƃ��ĔF���ł��܂��B�������A�b�҂̈Ӑ}�������Ƃ𐳂��������ł��邩�ǂ�����**��������**�A�ꍇ�ɂ���Ă͉^����ł��B�i[��������̉��߂��ł���u�����Ԃ�����H�ׂ��L�v���ʔ���](https://nihongonosensei.net/?p=7442)�j




����ł��ˁB�ʔ������ȕ��͂�����΂��Ў����Ă݂Ă��������B


# Appendix: getTokens �֐�
```matlab
function [listofTokens, chunkLinks] = getTokens(response)
% COTOHA API: Parse �̌��ʂ��� 
% 1: chunk�i���߁j�̌W��󂯊֌W��
% 2: �e token �i�`�ԑf�j��form �i�\�L�j�����o���֐� 

rsize = length(response.result);
chunkIDs = [];
IDs = [];
forms = [];
% chunkLinks �͗אڍs��Ƃ��Ď��o���� digraph �ŉ������܂��B
% �ڍׁFhttps://jp.mathworks.com/help/matlab/ref/digraph.html
chunkLinks = zeros(rsize);

% chunk ���Ƃɍ\���̂Ƃ��ď�񂪊m�ۂ���Ă��邽��
% 1�Â������Ă����܂��B
for ii = 1:rsize
    % 1 chunk ��
    tmp = response.result(ii);

    % ���� chunk "��"�������Ă��� chunkID
    head = response.result(ii).chunk_info.head;
    if head > 1 % ������ -1 �F����
        chunkLinks(ii,head) = 1; % 
    end
    % ���� chunk "��"�������Ă��� chunkID
    links = response.result(ii).chunk_info.links;
    if ~isempty(links) % �������Ă��Ȃ��ꍇ������
        linkorigins = [links.link]+1;
        chunkLinks(linkorigins,ii) = 1;
    end
    
    % chunk ���̌`�ԑf token ����������
    csize = length(tmp.tokens); % token �̐�
    chunkIDs = [chunkIDs; repmat(ii,csize,1)]; % ���� chunkID �𕡐�
    
    if csize == 1 
        % token ��1�̏ꍇ�͍\���̃f�[�^
        IDs = [IDs; tmp.tokens.id];
        forms = [forms; string(tmp.tokens.form)];

    else   
        % token ��2�ȏ�̏ꍇ�͍\���̂� cell �z��ɓ����Ă��܂��B
        IDs = [IDs; cellfun(@(x) x.id, tmp.tokens)];
        tmp = cellfun(@(x) x.form, tmp.tokens, 'UniformOutput', false);
        forms = [forms; string(tmp)];
        % �Q�l�F��Ɠ��������� for ���[�v�ŏ������ꍇ
        %  for jj = 1:csize 
        %      chunkIDs = [chunkIDs; ii];
        %      IDs = [IDs; tmp.tokens{jj}.id];
        %      forms = [forms; string(tmp.tokens{jj}.form)];
        %  end
    end
end

listofTokens = table(chunkIDs, IDs, forms);

end
```
