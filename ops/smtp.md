# Kikin SMTP correo apachiq sirwiqta ruway

## ñawpaq rimay

SMTP chiqalla puyu ranqhaqkunamanta yanapakuykunata rantiyta atin, kayhina:

* [Amazon SES SMTP nisqa](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali phuyu correo electrónico tanqay](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

Kikin correo servidorniykitapas ruwayta atikunki - mana k'uchuyuq kachay, pisi tukuy qullqi.

Uraypi, llamk'aymanta llamk'ayman rikuchiyku imayna kikin correo servidorniyku ruwayta.

## Servidor akllay

Kikinmanta qusqa SMTP sirwiq huk IP llapapaq munan 25, 456 chaymanta 587 kichasqa puertokunayuq.

Sapa kuti llamk'achisqa llaqta phuyukuna kay puertokunata ñawpaqmanta hark'arqanku, chaymanta kichay atikunman huk llamkana kamachiyta quspa, ichaqa ancha sasachakuyniyuq tukuymanta qhipaman.

Huk qutumanta rantiyta yuyaychani mayqinchus kay puertokuna kichasqa kachkan chaymanta yanapakun inverso dominio sutikuna churayta.

Kaypiqa, [Contabo](https://contabo.com) nisqatam yuyaychani.

Contabo huk quq quqmi, Munich llaqtapi, Alemania suyupi, 2003 watapi kamasqa, ancha atipanakuy chaninkunawan.

Sichus Euro rantiy qullqi hina akllanki, chanin aswan barato kanqa (huk servidor 8GB yuyarinayuq chaymanta 4 CPUs kaqwan yaqa 529 yuanes watapi qullqita qun, chaymanta qallariy churana qullqi huk watapaq mana qullqiyuq).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Huk kamachiyta churachkaspa, remark `prefer AMD` , chaymanta AMD CPU kaqwan sirwiq aswan allin ruwayniyuq kanqa.

Kay qatiqpi, Contabo kaqpa VPS kaqninta huk ejemplo hina hapisaq imayna kikiyki correo servidor ruwayta qawachinaypaq.

## Ubuntu sistema nisqap wakichiynin

Kaypi llamk'ana llikam Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Sichus ssh kaqpi servidor rikuchin `Welcome to TinyCore 13!` (urapi siqipi rikuchisqa hina), chaymi niyta munan sistema manaraq churasqachu kasqanmanta. Ama hina kaspa, ssh nisqamanta t'aqay hinaspa huk iskay kimsa minutukunata suyay musuqmanta yaykunaykipaq.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

`Welcome to Ubuntu 22.04.1 LTS` rikhuriptin, qallariy tukusqaña, chaymanta kay qatiq ruwanakunawan qatiyta atikunki.

### [Akllasqa] Wiñariy pachata qallariy

Kay ruwayqa munasqallam.

Allin kananpaq, ubuntu software kaqpa churayninta chaymanta sistema ruwayninta [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) kaqpi churani.

Kay kamachiyta purichiy huk ñit'iywan churanaykipaq.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Chinamanta llamkaqkuna, ama hina kaspa kay kamachiyta rantinpi llamk'achiy, chaymanta simi, pacha kiti, hukkunapas kikillanmanta churasqa kanqa.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo IPV6 nisqaman atichin

IPV6 atichiy chaymanta SMTP IPV6 direccionkunayuq correo electrónicokunatapas apachiyta atin.

`/etc/sysctl.conf` nisqapi llamk'apuy

Kay chirukunata tikray utaq yapay

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

[Contabo yachachiywan qatipay: IPv6 tinkiyta sirwiqniykiman yapay](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

`/etc/netplan/01-netcfg.yaml` llamk'apuy , huk pisi chirukunata yapay uray siqipi rikuchisqa hina (Contabo VPS ñawpaqmanta wakichiy willañiqiqa kay chirukunatañam kachkan, mana rimaylla).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Chaymanta `netplan apply` chay tikrasqa ruwayta ruwanapaq.

Wakichiy allin ruwasqa kaptin, `curl 6.ipw.cn` llamk'achiy atikunki hawa llikaykipa ipv6 direccionninta qhawanaykipaq.

## Clonar chay configuración waqaychasqa ops

```
git clone https://github.com/wactax/ops.soft.git
```

## Huk mana qullqiyuq SSL certificadota ruway kamachiy sutiykipaq

Correo apachiyqa huk SSL certificadota munan chifrasqapaq chaymanta firmanapaq.

[acme.sh](https://github.com/acmesh-official/acme.sh) nisqawanmi certificadokunata ruwanchik.

acme.sh nisqaqa kichasqa qullqisapa makiwan ruwasqa certificado firmanapaq yanapakuymi,

Wakichiy waqaychana ops.soft kaqman yaykuy, `./ssl.sh` purichiy, chaymanta huk `conf` qillqana mayt'u ruwasqa kanqa **pata willañiqipi** .

DNS quqniykita maskay [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) kaqmanta, `conf/conf.sh` llamk'achiy.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Chaymanta `./ssl.sh 123.com` purichiy `123.com` chaymanta `*.123.com` certificadokuna dominio sutiykipaq ruwanapaq.

Ñawpaq puriyqa kikinmanta [acme.sh](https://github.com/acmesh-official/acme.sh) churanqa chaymanta huk programasqa ruwayta yapanqa kikillanmanta musuqyachiypaq. `crontab -l` rikunki, kayhina chiruqa kanmi.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

Ruwasqa certificadopaq ñanqa imapas `/mnt/www/.acme.sh/123.com_ecc。`

Certificado musuqyachiyqa `conf/reload/123.com.sh` qillqa mayt'uta waqyanqa, kay qillqa mayt'uta llamk'achiy, kamachiykunata yapayta atikunki kayhina `nginx -s reload` kaqwan tupaq ruwanakuna certificado waqaychasqa musuqchaypaq.

## SMTP sirwiqta chasquid kaqwan ruway

[chasquid](https://github.com/albertito/chasquid) nisqaqa huk kichasqa qullqisapa SMTP sirwiqmi , Go simipi qillqasqa.

Ñawpa correo servidor programakuna Postfix chaymanta Sendmail kaqhina sustituto hina, chasquid aswan sasallawan chaymanta aswan sasa llamk'anapaq, chaymanta iskay kaq wiñachiypaq aswan facil.

Run `./chasquid/init.sh 123.com` huk ñit'iywan kikinmanta churasqa kanqa (123.com kachasqa kamachiy sutiykiwan tikray).

## Correo electrónico firma DKIM kaqmanta ruway

DKIM llamk'achkan correo electrónico firmakunata apachinapaq, cartakuna mana spam hina qhawasqa kananpaq.

Kamachiy allinta purisqanmanta, DKIM qillqata churanaykipaq mañasunki (urapi rikuchisqa hina).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Huk TXT registro DNS kaqman yapaylla (urapi rikuchisqa hina).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Servicio estadota & registrokunata qhaway

 `systemctl status chasquid` Servicio estadota qhaway.

Normal operación nisqapa estadonqa uraypi siqipi qawasqa hinam

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` icha `journalctl -xeu chasquid` pantasqa registrota qhawayta atin.

## Kamachiy suti churayta kutichiy

Inverso dominio sutiqa IP tiyayta tupaq kamachiy sutiman allichasqa kananpaq saqinapaqmi.

Huk kuti kamachiy sutita churayqa hark'anmanmi correo electrónicokuna spam hina riqsichisqa kananta.

Correo chaskisqa kaqtin, chaskiq sirwiq kutichisqa kamachiy suti t'aqwiyta ruwanqa kachaq sirwiqpa IP tiyayninpi, kachaq sirwiq allin kutichiy kamachiy sutiyuq kasqanmanta takyachinapaq.

Sichus kachaq sirwiq mana huk kutichiy kamachiy sutiyuqchu utaq sichus qhipa kamachiy suti mana kachaq sirwiqpa IP tiyayninwan tupanchu, chaskiq sirwiqqa correo electrónicota mana allin ruway hina riqsinman utaq mana chaskinmanchu.

[https://my.contabo.com/rdns](https://my.contabo.com/rdns) nisqaman yaykuy hinaspa uraypi rikuchisqa hina ruway

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

Inverso dominio sutita churasqamanta, yuyariy ipv4 chaymanta ipv6 dominio sutipa ñawpaqman resolucionninta servidorman ruwayta.

## chasquid.conf nisqap qutunpa sutinta llamk'apuy

`conf/chasquid/chasquid.conf` kaqmanta tikray kamachiy sutip chaninman.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Chaymanta `systemctl restart chasquid` purichiy yanapakuyta wakmanta qallarichinapaq.

## Conf git waqaychasqaman waqaychasqa

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Ejemplopaq, conf carpetata kikiypa github ruwayniyman kayhinata copia de seguridad ruwani

Ñawpaqtaqa sapanchasqa almacén nisqa ruway

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Conf directorioman yaykuy hinaspa almacén nisqaman apachiy

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Kachaq yapay

paway

```
chasquid-util user-add i@wac.tax
```

Kachaqta yapayta atin

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Yaykuna rimay allin churasqa kasqanmanta chiqaqchay

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

Ruwaq yapaymanta, `chasquid/domains/wac.tax/users` musuqchasqa kanqa, yuyariy almacénman apachiyta.

## DNS yapay SPF qillqata

SPF ( Sender Policy Framework ) nisqaqa huk correo electrónico chiqaqchay tecnologia , correo electrónico pantayta hark'anapaq llamk'achisqa.

Huk correo kachaqpa kikin kayninta chiqaqchan, kachaqpa IP tiyaynin DNS registrokunawan tupan chaymanta dominio sutiwan tupan chayta qhawaspa, engañaqkuna llulla correo electrónicokuna apachiyta harkan.

SPF registrokuna yapayqa harkanman correo electrónicokuna spam hina riqsisqa kanankupaq aswan atisqa.

Sichus dominio suti sirwiqniyki mana SPF laya yanapanchu, TXT laya qillqata yapaylla.

Ejemplopaq, `wac.tax` nisqapa SPF nisqanqa kayhinam

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF `_spf.wac.tax` nisqapaq

`v=spf1 a:smtp.wac.tax ~all`

Reparay kaypi `include:_spf.google.com` nisqayuq kasqayta, kayqa `i@wac.tax` Google correo cajapi apachiq direccion hina qhipaman ruwasqayrayku.

## DNS nisqa wakichiy DMARC

DMARC nisqaqa (Dominio nisqapi ruwasqa Willayta Chiqaqchay, Willakuy & Huñunakuy) nisqap pisichasqanmi.

SPF kutichiykunata hap'inapaq llamk'achkan (ichapas wakichiy pantasqakunarayku, icha huk runa qam hina ruwasqa kachkan mana allin apachiypaq).

TXT qillqasqata yapay `_dmarc` , .

Contenidoqa kayhinam

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

Sapa parámetro nisqapa significadonqa kayhinam

### p (Política) .

Imayna correo electrónicos llamk'achiyta rikuchin mayqinkunachus SPF (Kachaq kamachiy marco) utaq DKIM (DomainKeys Identified Mail) chiqaqchayta mana atikunkuchu. p parámetro nisqataqa kimsa chanikunamanta hukninmanmi churachwan:

* mana imapas: Mana ima ruwaypas ruwasqachu, chiqaqchay ruwasqalla apachiqman kutichisqa correo electrónico willay mecanismo kaqnintakama.
* Cuarentena: Mana chiqaqchayta pasaq correota spam carpetaman churay, ichaqa mana chiqamanta correota qhisachanqachu.
* mana chaskiy: Chiqamanta qhisachay correo electrónicos mana chiqaqchayta atiq.

### fo (Akllanakuna mana allin ruway) .

Willay mecanismopa kutichisqan willayta hayk'a kaqta willan. Kay chanikunamanta hukninmanmi churakunman:

* 0: Llapa willakuykunapaq chiqapchaypa rurunkunata willay
* 1: Chiqaqchayta mana atiq willakuykunatalla willay
* d: Domain suti chiqaqchay pantasqakunalla willay
* s: SPF chiqaqchay mana allin kasqanmanta willaylla
* l: DKIM chiqaqchay pantasqakunalla willay

### rua & ruf

* rua (Huñusqa willakuykunapaq URI willay): Huñusqa willakuykunata chaskinapaq correo electrónico direccion
* ruf (URI willakuy Forense willakuykunapaq): correo electrónico dirección detallada willakuykunata chaskinapaq

## MX registrokunata yapay correo electrónicos Google Mail kaqman apachinapaq

Imaraykuchus mana huk qullqipaq empresa correo cajata tariyta atirqanichu mayqinchus universal direccionkunata yanapan (Catch-All, ima correo electrónicos kay dominio sutiman apachisqa chaskiyta atin, mana ñawpaq simikuna hark'ayniyuq), chasquid llamk'achirqani llapa correo electrónicos Gmail correo cajayman apachinaypaq.

**Sichus kikiyki qullqiyuq negocio correo cajayuq kanki, ama hina kaspa ama MX kaqmanta tikraychu chaymanta kay ruwayta saltay.**

llamk'apuy `conf/chasquid/domains/wac.tax/aliases` , kachay qillqana mayt'u churay

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` llapa correo electrónicos nisqakunata rikuchin, `i` nisqaqa hawapi ruwasqa kachaqpa correo electrónico direccionninpa ñawpaqninmi. Correo apachinapaq, sapa llamk'achiq huk chiruta yapanan tiyan.

Chaymanta yapay MX registro (kaypi chiqanmanta señalani reverso dominio sutip direccionninta, imaynachus ñawpaq chirupi rikuchikun kay urapi siqipi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

Wakichiy tukusqa kaptin, wak correo electrónico direccionkunata llamk'achiy atikunki correo electrónico `i@wac.tax` kaqman chaymanta `any123@wac.tax` kaqman apachinaykipaq qhawanaykipaq sichus correo electrónicos Gmail kaqpi chaskiyta atikunki.

Mana hina kaqtinqa, chasquid registro nisqapi qhaway ( `grep chasquid /var/log/syslog` ).

## Google Mail nisqawan i@wac.tax nisqaman huk correo electrónico nisqa apachiy

Google Mail chay correota chaskisqanmanta, naturalmente suyarqani kutichiyta `i@wac.tax` kaqwan i.wac.tax@gmail.com kaqmanta.

[https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) kaqman yaykuy chaymanta "Huk correo electrónico direccionta yapay" ñit'iy.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Chaymanta, chay correo electrónico chaskisqa chiqaqchay codigota qillqay mayqinmanchus apachisqa karqa.

Tukuchanapaq, ñawpaqmanta kachaq tiyay hina churasqa kanman (kikillan tiyaywan kutichiy akllanawan kuska).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

Kayhina, SMTP correo servidorpa sayariyninta tukurqayku chaymanta kikin pachapi Google Mail llamk'achiyta correo electrónicokuna apachiypaq chaymanta chaskiypaq.

## Prueba correo electrónicota apachiy, wakichiy allinchu icha manachu chayta qhawanaykipaq

`ops/chasquid` nisqaman yaykuy

`direnv allow` (direnv ñawpaq huk llave qallariy ruwaypi churasqa chaymanta huk gancho shell kaqman yapasqa)

chaymantataq phaway

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

Chay parámetros nisqapa significadonqa kayhinam

* llamk'achiq: SMTP llamk'achiqpa sutin
* pasay: SMTP contraseña
* a: chaskiq

Prueba correo electrónicota apachiyta atinki.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

Gmail llamk'achiyta yuyaychakun prueba correo electrónicos chaskinapaq, ruwanakuna allinchu icha manachu chayta qhawanapaq.

### TLS kamachiy chifrasqa

Uraypi siq'ipi rikuchisqa hina, kay huch'uy wichq'ana kan, chaytaq niyta munan SSL certificado allinta atichisqa.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Chaymanta ñit'iy "Correo electrónico originalta rikuchiy".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

Uray siqipi rikuchisqa hina, Gmail original correo p'anqa DKIM rikuchin, chaymanta DKIM ruway allin kasqanmanta niyta munan.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Ñawpaq correo electrónico umalliqninpi Chaskisqa qhaway, chaymanta kachaqpa direccionnin IPV6 kaqta qhawayta atikunki, chaymanta IPV6 allin ruwasqa kaqtapas niyta munan.
