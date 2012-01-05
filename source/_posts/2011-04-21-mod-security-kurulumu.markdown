---
layout: post
title: RHEL 5.2 üzerinde mod_security kurulumu

---

Öncelikle şu paketleri kurmamız gerekiyor:

* pcre-devel
* apr-devel
* apr-util-devel
  
`sudo yum install pcre-devel apr-devel apr-util-devel`

Başlangıç için OWASP tarafından hazırlanan kural setlerini kullanacağız:

[http://sourceforge.net/projects/mod-security/files/modsecurity-crs](http://sourceforge.net/projects/mod-security/files/modsecurity-crs)

adresinden en son sürümü indirip, bu dosyayı

*/usr/local/apache2/conf/extra/modsecurity.d* dizini altına açarız.

*modsecurity_crs_10_config.conf.example* dosyasını
*modsecurity_crs_10_config.conf* adıyla kaydedip

`SecRuleEngine On`

satırını ekleriz.

Şimdi, Apache'yi durduralım:

*/usr/local/apache2/bin/httpd -k stop*  

Apache üzerinde *mod_unique_id* modülü kurulu olmalı.
Bu modülü kurmak için [apxs](http://httpd.apache.org/docs/current/programs/apxs.html
 "apxs")'i kullanabiliriz:  

`sudo /usr/local/apache2/bin/apxs -i -a -c /usr/local/src/httpd-2.2.17/modules/metadata/mod_unique_id.c`

Artık mod_security'yi derleyebiliriz:

    tar zxvf modsecurity-apache_2.5.13.tar.gz
    cd modsecurity-apache_2.5.13  
    cd apache2  
    ./configure  
    make  
    sudo make install  

*/usr/local/apache2/conf/httpd.conf* içerisine şu satırları ekleriz:

    LoadFile /usr/lib/libxml2.so  
    LoadModule security2_module modules/mod_security2.so  
    Include conf/extra/modsecurity.d/modsecurity_crs_10_config.conf  

Kurulumu tamamlamış olduk, Apache'yi tekrar çalıştırabiliriz:

*/usr/local/apache2/bin/httpd -k start*
