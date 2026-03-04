1. Uygulamanın Amacı
Bu deneyde, STM32F407 mikrodenetleyicisinin GPIO (General Purpose Input Output) birimini kullanarak dijital çıkış (LED kontrolü) ve dijital giriş (Anahtar/Buton okuma) işlemlerinin öğrenilmesi amaçlanmaktadır.

2. Kullanılacak Donanım ve Pin Bağlantıları
ARM App Deney Kiti üzerinde bulunan 8-Bit LED devresi, Menü Buton Takımı ve Slide Switch devreleri kullanılacaktır.

Bileşen	Pin Kodu	Mode	Açıklama
LED 0 - 7	PE0 – PE7	GPIO_Output	Kara Şimşek efekti için 8 adet kırmızı LED
Slide Switch 0 (SW0)	PE13	GPO_Input	Tüm LED’leri Yakma
Slide Switch 1 (SW1)	PE14	GPO_Input	Kara Şimşek animasyonu durdurma
Slide Switch 2 (SW2)	PE15	GPO_Input	Kara Şimşek animasyon hız ayarı

SW3 ve SW2’nin ikilik tabanda alacağı 4 farklı duruma karşılık 4 farklı hız kademe ayarı! 
Slide Switch 3 (SW3)	PB15	GPO_Input	
Slide Switch 4 (SW4)	PC8	GPO_Input	Kara Şimşek animasyonu için Otomatik / Manuel kontrol mod seçimi.
Menü Buton Left	PD12	GPO_Input	Manuel kontrol modunda iken yanan ledi 1 birim sola kaydır.
Menü Buton Right	PD14	GPO_Input	Manuel kontrol modunda iken yanan ledi 1 birim sağa kaydır.


3. UYGULAMA İSTERLERİ
ARM App Deney Kiti üzerinde bulunan 8-Bit LED devresini, Menü Buton Takımını ve Slide Switchleri kullanarak Otomatik / Manuel kontrol edilebilir Kara Şimşek uygulamasını gerçekleştirmeniz istenmektedir. Temel gereksinimler;

•	Öncelikle Slide Switch 4 (SW4)’ün lojik durumu 0 iken otomatik, 1 iken manuel kontrol modunun aktif olması.

•	Otomatik kontrol modunda, Kara Şimşek animasyonunun oluşturulması için LED’lerin sağdan sola (0 to 7) ve soldan sağa (7 to 0) sırayla birim zamanda yalnızca ilgili indisteki LED’in yanması ve devam eden döngü içerisinde bu indisin güncellenmesi,

•	Slide Switch 0 (SW0) aktif iken (lojik-1), tüm LED’lerin (LED 0 - 7) yanması ve pasif konuma geçtiği zaman tekrar kaldığı yerden devam etmesi,
•	Slide Switch 1 (SW1) aktif iken (lojik-1), Kara Şimşek animasyonunun durdurulması ve pasif konuma geçtiği zaman tekrar kaldığı yerden devam etmesi,

•	Hız kontrolü için kullanılacak olan Slide Switch 2/3 (SW2/SW3)’ün aşağıda verilen doğruluk tablosundaki lojik değerlerine göre Kara Şimşek animasyon hızının belirlenmesi. (x: LED’ler arası geçiş hızı, bekleme süresi ile ters ortantılı!)

SW3	SW2	Animasyon Hızı
0	0	x
0	1	2x
1	0	3x
1	1	0,5x
Lojik – 0: Pasif
Lojik – 1: Aktif


•	Manuel kontrol modunda, Menü Buton Takımda yer alan LEFT/RIGHT butonları aracılığı ile aktif olarak yanan LED’in 1-Bit sol veya sağ tarafa kayma (shift) işlemini gerçekleştirmesi,

•	Akitf olan LED, LED7 iken LEFT butonuna basılması durumunda aktif LED’in LED0 olması,

•	Akitf olan LED, LED0 iken RIGHT butonuna basılması durumunda aktif LED’in LED7 olması,

•	Slide Switch 4 (SW4)’ün değiştirilmesi ile Kontrol modları arasında geçiş yapılırken işlemlerin, Kara Şimşek animasyonunda en son aktif olan LED üzerinden devam etmesi gerekmektedir! 
