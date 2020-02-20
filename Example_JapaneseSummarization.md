# �͂��߂�
  


@aoimidori ����� [MATLAB����COTOHA API���R�[�����Ă݂�](https://qiita.com/aoimidori/items/644ac0e726d60a99cc4a) �Ɏh�����󂯁A���� MATLAB ���� COTOHA API �������Ă݂܂����B


  
> **CONOHA API �Ƃ́F**�\����́A�Ɖ���́A�L�[���[�h���o�A�����F���A�v��ȂǁA�l�X��**���R���ꏈ���E��������API**��񋟂��Ă���T�[�r�X�ł��B**NTT�O���[�v��40�N�ɂ킽�錤������**�ł���A���{�ꎫ����P���3000��ȏ�̈Ӗ������ނ���Z�p�Ȃǂ����p���A���x�ȉ�͂�API�Ŏ�y�ɗ��p�ł��܂��B


  


�Ƃ������Ƃł����A�����ȗV�т��ł������B�ł��邱�Ƃ���R�����Ă��ꂼ�ꎎ�������ł��ʔ����ł��B




@mosaosa ����� [��X�̃R�~���j�P�[�V�����ɂ�"��"������Ȃ��B](https://qiita.com/mosamosa/items/e63f6e582a206659dc2b) ���G��B��ŏ_��Ȕ��z���������Ȃ��Ǝv���܂����B




���͂���Ȑ��ȃA�C�f�A���o�Ă��Ȃ��̂ŁA�Ƃ肠���� COTOHA API �̊�{�@�\�ŗV��ł݂܂��B


  
# ���������


�܂��� Qiita �L���̗v��


  
## ���s��

   -  MATLAB R2019b 
   -  Text Analytics Toolbox 



COTOHA API ���g���܂ł̎菇�� @aoimidori ����̋L�����Q�l�ɂ��Ă��������B


# **0. �A�N�Z�X�g�[�N�����擾����**
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
# 1. Qiita �L���̓ǂݍ���


������ Qiita API ���g���Ď������ł������ł����A�܂��� URL ���璼�ړǂݍ���ł݂܂��傤�B[�e���v���[�g�g���� PowerPoint �X���C�h�쐬�������FMATLAB Report Generator ��](https://qiita.com/eigs/items/cb48fdcd741126d09def) ���Ɏg���Ă݂܂��B


```matlab
% �e���v���[�g�g���� PowerPoint �X���C�h�쐬�������FMATLAB Report Generator ��
URL = 'https://qiita.com/eigs/items/cb48fdcd741126d09def';
source = webread(URL);
source(1:100) % �`���� 100 ����
```
```
ans = '<!DOCTYPE html><html><head><meta charset="utf-8" /><title>�e���v���[�g�g���� PowerPoint �X���C�h�쐬�������FMATLAB Repo'
```


�\�[�X���當�͂�������Ă��܂��B�����Ŏg���̂� html ����e�L�X�g���o���� `extractHTMLText` �֐��i[�w���v�y�[�W](https://jp.mathworks.com/help/textanalytics/ref/htmltree.extracthtmltext.html)�j


```matlab
sourceText = extractHTMLText(source);
sourceText(1:200)
```
```
ans = 
    '�͂��߂�
     
     �V�S�g�ŁA����I�ɂƂ���W�v���p���|�ɓZ�߂Ă�����ł����AMATLAB �Ńf�[�^�W�߂āA�O���t���R�s�y���āE�E�Ȃ� 30�����������Ƃ��n���ɂ߂�ǂ������B
     
     �u�܂��A������邱�Ƃ���Ȃ����E�E�v�Ɖ䖝���Ă���Ă��܂������A2020�N�� �u�ދ��Ȃ��Ƃ� MATLAB �ɂ�点�悤�v�Ƃ������ƂŁA��O���N���Ď������B
     
     ���̍ۂɂ͂܂����_�ƁAPowerPoint �e���v���[�g�̎g�p�����'

```


�܁A�Ȃ񂩂悳�����B


# 2. COTOHA API �Ăяo��


COTOHA API ��[���t�@�����X](https://api.ce-cotoha.com/contents/reference/apireference.html)�ɂ���


> curl -X POST -H 'Content-Type:application/json;charset=UTF-8' -H 'Authorization:Bearer [Access Token]' -d '{"document":"�O���������m��ɒ�؂��Ă��܂��B����A���C�����瓇�ߊC�ɂ����āA�k���{���瓌���{�����₩�ɕ����Ă��܂��B�֓��n���́A���ꎞ�X�܂�A�Ƃ���ɂ��J�ƂȂ��Ă��܂��B�����́A��������C��O���̉e���ɂ��A�����܂�ŁA��͉J�ƂȂ�ł��傤�B","sent_len":"1"}' [API Base URL]/nlp/beta/summary




�Ƃ��������Ŏg���܂��B`sent_len` �͗v����A�����̕��͂ŕԂ����̃I�v�V�����̂悤�ł��B�K�{�̓��͂� `document` �Ȃ̂ŁA�����ɏ�Œ��o�������͓���Ă݂܂��B


  


POST �Ȃ̂� webwrite �֐��ł����܂��ˁB@aoimidori ����̃R�[�h���܂˂Ă݂�ƁE�E


```matlab
baseurl = 'https://api.ce-cotoha.com/api/dev/';
Header = {'Content-Type', 'application/json;charset=UTF-8';
    'Authorization', ['Bearer ' tokens.access_token]};
Body = struct('document', sourceText, ... 
          'sent_len', '1');
options = weboptions('RequestMethod','post', ...
    'MediaType','application/json','HeaderFields', Header);

response = webwrite([baseurl 'nlp/beta/summary'], Body, options);
```


�L���v��́E�E


```matlab
string(response.result)
```
```
ans = "MATLAB �R�[�h�F�������냌�|�[�g%% ���O�ݒ�% �t�@�C�����ɍ����̓��t���g���܂�reportDate = datetime; reportDate.Format = 'yyyy-MM-dd';% �֘A���C�u�����̓ǂݍ���import mlreportgen.ppt.*;% ���O�쐬�����e���v���[�g����X���C�h�쐬pres = Presentation(fileName,'sampleTemplate.potx');%% �^�C�g���X���C�h�쐬% �e���v���[�g�ɂ��� "Title Slide" ���C�A�E�g���g�ptitleSlide = add(pres,'Title Slide');% �t�@�C������^�C�g��fileName = "sampleReport" + string(reportDate);titleText = "�T���v�����|�[�g";subTitleText = "�쐬��" + string(reportDate);% �v���[�X�z���_�̓��e�����ւ�replace(titleSlide,'Title',titleText);replace(titleSlide,'Subtitle',subTitleText);%% �������烌�|�[�g�y�[�W% ��������� N ��U���āA�o��ڂ̉񐔂��W�v���܂��B"
```
# 3. �Ȃ񂩂��������F�R�[�h�̂���


����͂ǂ����L���� MATLAB �R�[�h���܂܂�Ă��邩��ł��ˁB����͎�菜�������B




���x�� HTML ���p�[�X���邽�߂� `htmlTree` �֐��i[�w���v�y�[�W](https://jp.mathworks.com/help/textanalytics/ref/htmltree.html)�j�g���Ă݂܂��B�\�[�X������ƁA�R�[�h�� `<div class="code-frame"> `�ň͂܂�Ă���݂����Ȃ̂ŁA


```matlab
tree = htmlTree(source);
```


�ł��̒�����A�p���O���t�A�w�b�_�[�A���X�g�Ȃǎ���Ă��܂��傤�B


```matlab
selector = "p,li";
subtrees = findElement(tree,selector);
subtrees(1:10) % ������Ƃ����\��
```
```
ans = 
  10x1 htmlTree:

    <P>�V�S�g�ŁA����I�ɂƂ���W�v���p���|�ɓZ�߂Ă�����ł����AMATLAB �Ńf�[�^�W�߂āA�O���t���R�s�y���āE�E�Ȃ� 30�����������Ƃ��n���ɂ߂�ǂ������B</P>
    <P>�u�܂��A������邱�Ƃ���Ȃ����E�E�v�Ɖ䖝���Ă���Ă��܂������A2020�N�� <STRONG>�u�ދ��Ȃ��Ƃ� MATLAB �ɂ�点�悤�v</STRONG>�Ƃ������ƂŁA��O���N���Ď������B</P>
    <P>���̍ۂɂ͂܂����_�ƁAPowerPoint �e���v���[�g�̎g�p����Љ�܂��B</P>
    <LI>MATLAB R2019b</LI>
    <LI>MATLAB Report Generator</LI>
    <P>����� MATLAB Report Generator ���g���܂��� <A href="https://jp.mathworks.com/matlabcentral/answers/99268-powerpoint" rel="nofollow noopener" target="_blank">COM �T�[�o�[���g�����@</A> �Ɋ���Ă���� MATLAB �����ł��ł���Ǝv���܂��B</P>
    <P>�ȑO������ <A href="https://qiita.com/eigs/items/8c4bf743fc1319762607" id="reference-e1a4b2e138fe2f4fffda">�yMATLAB�zPowerPoint �X���C�h�쐬������</A> �ł́A�@�B�w�K�̕]�����ʂ�Z�߂��Ƃ����������܂����B�����A�摜�̈ʒu�Ȃǂ����s���낵�ē��肵�āA�R�[�h���ɒ������B</P>
    <P>�\���ʒu�ȂǕύX�̕K�v��������Γ��ɍ���Ȃ��Ƃ͎v���܂����A�����e�i���X�I�Ɏc�O�ȗ�ł͂���܂����B�����܂���B����͏��������w�L�т��āAPowerPoint �̃e���v���[�g���g��������Љ�܂��B</P>
    <P>������ނ��v�����Ȃ������̂ł����A���ۂɖ��ɗ����ǂ����́A�F����̑z���͎���E�E�Ƃ������ƂŁA��������� <CODE>N</CODE> ��ӂ������ʂ��܂Ƃ߂�p���|����Ă݂܂����B</P>
    <P><DETAILS><SUMMARY>MATLAB �R�[�h�F�������냌�|�[�g</SUMMARY><DIV><DIV class="code-frame" data-lang="matlab"><DIV class="highlight"><PRE><SPAN class="c1">%% ���O�ݒ�</SPAN><SPAN class="c1">% �t�@�C�����ɍ����̓��t���g���܂�</SPAN><SPAN class="n">reportDate</SPAN><SPAN class="o">=</SPAN><SPAN class="nb">datetime</SPAN><SPAN class="p">;</SPAN><SPAN class="n">reportDate</SPAN><SPAN class="o">.</SPAN><SPAN class="n">Format</SPAN><SPAN class="o">=</SPAN><SPAN class="s1">'yyyy-MM-dd'</SPAN><SPAN class="p">;</SPAN><SPAN class="c1">% �֘A���C�u�����̓ǂݍ���</SPAN><SPAN class="nb">import</SPAN><SPAN class="n">mlreportgen</SPAN><SPAN class="o">.</SPAN><SPAN class="n">ppt</SPAN><SPAN class="o">.*</SPAN><SPAN class="p">;</SPAN><SPAN class="c1">% ���O�쐬�����e���v���[�g����X���C�h�쐬</SPAN><SPAN class="n">pres</SPAN><SPAN class="o">=</SPAN><SPAN class="n">Presentation</SPAN><SPAN class="p">(</SPAN><SPAN class="nb">fileName</SPAN><SPAN class="p">,</SPAN><SPAN class="s1">'sampleTemplate.potx'</SPAN><SPAN class="p">);</SPAN><SPAN class="c1">%% �^�C�g���X���C�h�쐬</SPA�c

```


`<div class="code-frame">` �ň͂܂ꂽ�R�[�h�͂Ȃ��Ȃ��Ă��܂����E�E���������̂�����܂��B


## 3.1 `<DETAILS>` ���ĂȂ�


����̓R�[�h��܂肽���ޕ\���ɂ��Ă���Ƃ���ł��ˁE�E




![image_0.png](Example_JapaneseSummarization_images/image_0.png)




�����B�����̃R�[�h�� <p> ���ɓ����Ă��Ă��܂��B�B���\�ɂ߂�ǂ������Ȃ��Ă����B




�܂肽����ł��Ȃ���΁A�����܂ł̏����ŏ\���Ȃ͂��B


  


���Ȃ݂ɂ��̂܂܎��s�����


```matlab
sentence = extractHTMLText(subtrees);
sentence = join(sentence); 
Body = struct('document', sentence, ... 
          'sent_len', '1');
options = weboptions('RequestMethod','post', 'MediaType','application/json','HeaderFields', Header);
response = webwrite([baseurl 'nlp/beta/summary'], Body, options);
string(response.result)
```
```
ans = "names = ["one","two","three","four","five","six"];for ii=1:5 % 10�� ���� 10����܂� N = 10^ii; % 1 ���� 6 �܂ł̐����𐶐� diceResults = randi(6,[N,1]); % ���ꂼ��̏o�ڂ̉񐔂��W�v counts = histcounts(diceResults); [countsSorted,idx] = sort(counts,'descend'); % �q�X�g�O�����v���b�g�쐬 hFigure = figure(1); histogram(diceResults,'Normalization','probability'); title('Histogram of Each Occurenace'); ha = gca; ha.FontSize = 20; % �摜�Ƃ��ĕۑ����Č�ɁA�p���|�ɃR�s�[ imgPath = saveFigureToFile(hFigure); pictureObj = Picture(imgPath); % �X���C�h�^�C�g�� slideTitle = "Uniformly Distributed? (N = " + string(N) + ")"; % ���O�ɏ������Ă����� Custom ���C�A�E�g����y�[�W�쐬 slide = add(pres, 'Custom'); replace(slide,'Title',slideTitle); % �^�C�g�� replace(slide,'Picture Placeholder Big', pictureObj); % �^�񒆂̓q�X�g�O������z�u % �o���񐔏��Ƀg�b�v�T�F�o���񐔂Ɖ摜��z�u topfive = names(idx); for jj=1:5 % �摜�͎��O�ɗp�ӂ������̂��g�p imagePath = "./images/" + topfive(jj) + ".png"; if ~exist(imagePath,'file') % �O�̂��߉摜���Ȃ��ꍇ imagePath = "./images/a.png"; end pictureObj = Picture(char(imagePath)); replace(slide,"Picture Placeholder " + jj, pictureObj); replace(slide,"Text Placeholder " + jj, string(countsSorted(ii))); end % hFigure ����� if( isvalid(hFigure) ) close(hFigure); endend%% �ȏ�̃y�[�W�����ƂɃp���|�쐬% msgbox �Ń_�C�A���O�o���Ă݂�hMsg = msgbox('Generating PowerPoint report...');% pres ����Ă����܂��B"
```


�ƈ��������c�O�Ȋ����ɂȂ�܂��B


## 3.2 �n���� `<DETAILS>` �΍�


�����͂Ƃɂ��������΂����Ƃ������ƂŁA��Â� `<DETAILS>` ������������Ă��邩�m�F���č폜���܂��B


```matlab
selector = "p,li";
subtrees = findElement(tree,selector);

% check if details contained in p
index = false(length(subtrees),1);
for ii=1:length(subtrees)
    tmp = findElement(subtrees(ii),'details');
    index(ii) = isempty(tmp); % <DETAILS> ������� false �ɂȂ�
end

% DETAILS ����
subtreesNoDetails = subtrees(index);
subtreesNoDetails(1:10)
```
```
ans = 
  10x1 htmlTree:

    <P>�V�S�g�ŁA����I�ɂƂ���W�v���p���|�ɓZ�߂Ă�����ł����AMATLAB �Ńf�[�^�W�߂āA�O���t���R�s�y���āE�E�Ȃ� 30�����������Ƃ��n���ɂ߂�ǂ������B</P>
    <P>�u�܂��A������邱�Ƃ���Ȃ����E�E�v�Ɖ䖝���Ă���Ă��܂������A2020�N�� <STRONG>�u�ދ��Ȃ��Ƃ� MATLAB �ɂ�点�悤�v</STRONG>�Ƃ������ƂŁA��O���N���Ď������B</P>
    <P>���̍ۂɂ͂܂����_�ƁAPowerPoint �e���v���[�g�̎g�p����Љ�܂��B</P>
    <LI>MATLAB R2019b</LI>
    <LI>MATLAB Report Generator</LI>
    <P>����� MATLAB Report Generator ���g���܂��� <A href="https://jp.mathworks.com/matlabcentral/answers/99268-powerpoint" rel="nofollow noopener" target="_blank">COM �T�[�o�[���g�����@</A> �Ɋ���Ă���� MATLAB �����ł��ł���Ǝv���܂��B</P>
    <P>�ȑO������ <A href="https://qiita.com/eigs/items/8c4bf743fc1319762607" id="reference-e1a4b2e138fe2f4fffda">�yMATLAB�zPowerPoint �X���C�h�쐬������</A> �ł́A�@�B�w�K�̕]�����ʂ�Z�߂��Ƃ����������܂����B�����A�摜�̈ʒu�Ȃǂ����s���낵�ē��肵�āA�R�[�h���ɒ������B</P>
    <P>�\���ʒu�ȂǕύX�̕K�v��������Γ��ɍ���Ȃ��Ƃ͎v���܂����A�����e�i���X�I�Ɏc�O�ȗ�ł͂���܂����B�����܂���B����͏��������w�L�т��āAPowerPoint �̃e���v���[�g���g��������Љ�܂��B</P>
    <P>������ނ��v�����Ȃ������̂ł����A���ۂɖ��ɗ����ǂ����́A�F����̑z���͎���E�E�Ƃ������ƂŁA��������� <CODE>N</CODE> ��ӂ������ʂ��܂Ƃ߂�p���|����Ă݂܂����B</P>
    <P/>

```
# 4. ����ǂ����v��
```matlab
sentence = extractHTMLText(subtreesNoDetails);
sentence = join(sentence);
Body = struct('document', sentence, ... 
          'sent_len', '1');
options = weboptions('RequestMethod','post', 'MediaType','application/json','HeaderFields', Header);
response = webwrite([baseurl 'nlp/beta/summary'], Body, options);
string(response.result)
```
```
ans = "����͏��������w�L�т��āAPowerPoint �̃e���v���[�g���g��������Љ�܂��B"
```


�ł����I�I�^�C�g���ƍ��킹��Ɠ��e�Ƃ����Ă��܂��ˁB


# 5. ���̋L�����v��


`getSummary` �֐��ɂ��āi�\�[�X�̓y�[�W���L�j���̋L���ɂ������Ă݂܂��B��O�����ŗv�񕶂̐����w�肷��悤�ɂ��܂����B




[**�yMATLAB�z�@�B�w�K�A�v����̃v���b�g���Č���������ł����E�E**](https://qiita.com/eigs/items/38e31027529f92233b27)


```matlab
URL = 'https://qiita.com/eigs/items/38e31027529f92233b27';
source = webread(URL);
summary = getSummary(source, tokens, 1)
```
```
summary = "�iMATLAB Answers: �u��A�w�K���p���ė\���������v���b�g�f�[�^���̉����̒l�̏o�́v�����p�j �Ƃ��A CSV�t�@�C������C���|�[�g�����f�[�^��p���ĉ�A�w�K����g�p������,�o�͂���鉞���v���b�g�̒l�Ɗ֐����o�͂���ɂ͂ǂ�����Ηǂ��ł��傤���D�iMATLAB Answers: �u��A�w�K��̉����v���b�g�ɂ��āv�����p�j �ȂǁA�A�v����̌��ʂ��Č��������A���ɂ����p�������Ƃ�����������܂��B"
```


�܂��A�A�킩�邩�E�E�E�B




[**MATLAB����COTOHA API���R�[�����Ă݂�**](https://qiita.com/aoimidori/items/644ac0e726d60a99cc4a)




@aoimidori ����̋L��


```matlab
URL = 'https://qiita.com/aoimidori/items/644ac0e726d60a99cc4a';
source = webread(URL);
summary = getSummary(source, tokens, 1)
```
```
summary = "MATLAB�R�[�h�͉��L�B"
```


�ނށE�E�H�m���� MATLAB �ł̎��s�T���v�����L���̃��C���ł͂���B


```matlab
summary = getSummary(source, tokens, 2)
```
```
summary = "MATLAB�R�[�h�͉��L�B ������̌������t�@�����X�̂����ɉ����āA�����ɍ\����͂����Ă݂܂��B"
```


2 ���ɂ���Ɗm���ł����ˁB




[**�yMATLAB�zOutlook����\��\���擾����**](https://qiita.com/motorcontrolman/items/03ea4d2a978d626f4337)




@motorcontrolman ����̍ŋ߂̋L�����i����Ɂj�܂Ƃ߂��Ⴂ�܂��B


```matlab
URL = 'https://qiita.com/motorcontrolman/items/03ea4d2a978d626f4337';
source = webread(URL);
summary = getSummary(source, tokens, 2)
```
```
summary = " �擾�̑ΏۂƂȂ�Outlook�\��\�͉��L�ł��B �֗����Ȃ�(����) �ŏI�S�[����Subject����e�L�X�g�f�B�[�v���[�j���O�ŋƖ����e��ސ��A�Ɩ����ׂ������鉻���邱�Ƃł��B"
```


�l�N�X�g�X�e�b�v�ɂ܂łӂ�Ă�I




[**MATLAB�ŋ����̉�͂��n�߂悤�i�L���Ȕ����������Ă݂悤�j**](https://qiita.com/teruqii/items/447d09d10e24fca0c20f)




���[�^�[�{�[�g�}������ @teruqii ����̋L�����ƁE�E


```matlab
URL = 'https://qiita.com/teruqii/items/447d09d10e24fca0c20f';
source = webread(URL);
summary = getSummary(source, tokens, 3)
```
```
summary = "�R�A���ɂ��ĂR�_���炢�����Ă݂悤���ȁB ������ ���ʁB 1��ځF100�~ �͂��� 2��ځF200�~ �͂��� 3��ځF300�~ �͂��� 4��ځF400�~ ������I �� �z���R�{�� 1200�~�Q�b�g 5��ځF300�~ ������I �� �z���R�{�� 900�~�Q�b�g 6��ځF200�~ �͂��� 7��ځF300�~ �͂��� �Ƃ��������B"
```


�Ƃ肦�����ׂ����������H���o�Ă��܂��ˁI


# �܂Ƃ�


Qiita �L���Ȃ�ł́i�H�j�Ȃ̂��v���O�����R�[�h�����̎�舵���Ɏ�Ԏ��܂����A�A�����������ɗv�񂳂�Ă��܂��ˁB�L����񎩑̂� Qiita API �Ŏ���Ă����̂ŁA���ɂ����낢��V�ׂ����ȋC�����܂��B




�A�C�f�A����ł͂��Ȃ�ʔ������ƂɂȂ肻���ICOTOHA API �������Ă݂����I�Ƃ������̂����ɗ��Ă���������ł��B


# getSummary �֐�
```matlab
function summary = getSummary(htmlSource, tokens, sent_len)

tree = htmlTree(htmlSource);

selector = "p,li";
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
