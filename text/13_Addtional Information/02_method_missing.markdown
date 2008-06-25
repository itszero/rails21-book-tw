## �ϥ�method\_missing�ɽФp��

�ѩ�Ruby�O�ʺA�y���A�o�˴N�ϱo**respond\_to?**�D�`���n�A�A�O�_�g�`�ˬd�Y�Ӫ���O�_�֦��Y�Ӥ�k�H�A�O�_�g�`�ϥ�**is\_a?**���ˬd�Y�Ӫ���O�_�O�ڭ̩һݭn���H


�M�ӡA�H�̱`�`�ѰO�o�˰��A���Ӭݭ�**method\_missing**���Ҥl�a�G

    class Dog
        def method_missing(method, *args, &block)
            if method.to_s =~ /^bark/
                puts "woofwoof!"
            else
                super
            end
        end
    end

    rex = Dog.new
    rex.bark #=> woofwof!
    rex.bark! #=> woofwoof!
    rex.bark_and_run #=> woofwoof!

�ڷQ�A�֩w���D**method\_missing**�I�b�W�����Ҥl���ګإߤF�@��**Dog**���O������A�M��I�s�T�Өä��s�b����k�G**bark**, **bark!**�P**bark\_and\_run**�A���N�|�h�I�s**method\_missing**���ӧڥΥ��W��F���W�w���u�n�Obark�}�Y�N��X"woofwoof!"�C

�ݰ_�ӨS������D�a�H������~��ݬݧڥ�**respond\_to?**���ˬd�G

    rex.respond_to? :bark #=> false
    rex.bark #=> woofwoof!

�ݨ�F�ܡH����^false�A�]�N�O�����{���ӹ���èS��bark��k�A���H�O�ɭԨӫ��ӧڭ̪��W�h�ӧ���**respond\_to?**�F�I

    class Dog
    METHOD_BARK = /^bark/
        def respond_to?(method)
            return true if method.to_s =~ METHOD_BARK
        super
        end
        def method_missing(method, *args, &block)
            if method.to_s =~ METHOD_BARK
                puts "woofwoof!"
            else
                super
            end
        end
    end
    rex = Dog.new
    rex.respond_to?(:bark) #=> true
    rex.bark #=> woofwoof!

 

OK�I�d�w�F�I�o�˪����D�bRails�����M�s�b�A�A�i�H�ոլݥ�**respond\_to?**���ˬd**find\_by\_xxx**�N�ܩ��դF�C

Ruby���X�i�ʯ����H�٩_�A���O�p�G�@���`�N�N�����|��ۤv�d�o�@�Y�����C

��M�A���Ӥw�g�q��ڭn������F�A�bRails 2.1���o�Ӱ��D�w�g�״_�F�A���H���ܧA�@�˥i�H�ոլݥ�**respond\_to?**���ˬd**find\_by\_xxx**