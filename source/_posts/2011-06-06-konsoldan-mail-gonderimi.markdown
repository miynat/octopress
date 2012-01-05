---
layout: post
title: Konsoldan mail gönderimi

---

Konsoldan mail göndermek için **mutt**’ı kullanabiliriz.

[*Mutt*](http://mutt.blackfish.org.uk/ "Mutt"), metin-tabanlı bir mail istemcisidir.

`yum -y install mutt`

ile kurulumu yapıp

`echo "Mail içeriği " | mutt -a eklenti.gz -s "Konu" -- selcukmiynat@gmail.com`

komutuyla mail gönderebiliriz.

Komutu kısaca incelersek:

**echo “Mail içeriği“** : Bu komutla mail’in içeriğini veriyoruz.  
**-a** : Eklenti(attachment) göndermek için bu parametreyi kullanıyoruz.  
**-s** : Mail'in konusunu belirtmek için kullanılan parametre  

Alıcı mail adresinden önce -- (çift tire) kullanmazsak şöyle bir hata alabiliriz, buna da dikkat etmek gerek:  
*Can't stat selcukmiynat@gmail.com: No such file or directory*  
*selcukmiynat@gmail.com: unable to attach file.*
