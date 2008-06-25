## Cross-Site Scripting�����m

�bRails 2.0��*application.rb*�����Ӵ��d�N�L�H�U�{���X�a�H

    class ApplicationController < ActionController::Base
       helper :all
       protect_from_forgery
    end

�Ъ`�N�W���o�q�{���X����**protect\_from\_forgery**���I�s�C

�Ať���L��(XSS)�ܡH�̪�@�q�ɶ�XSS������q����A�N�ثe�Ө��b�j�h�ƪ��������Φh�Τֳ��s�b��XSS���|�}�F��XSS�|�}�|�Q�@���h���c�N���H�Q�ΡA�i�H�Ψӭק�������e�B�����A�Ʀܳq�LJavaScript�ӱ����L�Τ᪺�s���������C���ާ����覡���P�A���O��D�n���ت����O�ϥΤ�b�����������A�U���X�@�Ǩ��c�����ڳ��Q���X�Ӫ��Ʊ��C�̷s��������q�N�s��"Cross-Site Request Forgery"�C

Cross-Site Request Forgery�P�e���һ���XSS��z�t���h�A���O�󦳦M�`�ʡA�H��Ajax���y��A�����|�}���Q�ΪŶ��P��k��[�F���I(�ɥR�G���峹²�餤�媩½Ķ�̦b���e���g�F�@�g����CSRF���峹�A��ĳ�@Ū�GCSRF: ���n�C���F�ڪ��M�`�M��?��O)

protect_from_forgery�ΨӽT�O�t�α����쪺���T�����Ӧ۩�t�Υ����A�Ӥ��|�O�q�ĤT��ǰe�L�Ӫ��F�갵����z�O�b��椤�PAjax�ШD���K�[�@�Ӱ��Session���Х�(token)�AController�����檺��T�ɷ|�ˬd�o��Token�O�_�ǰt�H�M�w�p��^���o��Post�ШD�C

���L�o�Ӥ�k�ä��O�@�HGet���D���ШD�A���O�]�S���Y�AGet�D�n�N�O���F�n�D��ơA�Ӥ��|�ק���Ʈw���C

�p�G�A�Q��h���F��CSRF (Cross-Site Request Forgery)�A�аѦҩ��U�X�Ӻ��}�G

    * http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750
    * http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750
    * (�A�h�@�ӡG�e���Ҥ��Ъ��mCSRF: ���n�C���F�ڪ��M�`�M��?��O�n�C)

���԰O�A����k�ä�����U�L�@���A�N�����`�ڭ̳����w�������ˡG�L�ä��O�ȼu�I(It's not a silver bullet)