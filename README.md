# Twitter Kategori Tahmini

<br/>

Bir sınıflandırma algoritmasıdır. Twitterdan alınmış olan farklı kategorilerdeki (Siyaset, Ekonomi, Spor, Teknoloji ve Bilim) tweetleri ile model eğitiliyor ve modele bir tweet gönderildiğinde bunun hangi kategoride bir tweet olduğunu tespit ediyor. Bu algoritma sayesinde bir twitter hesabının daha çok hangi alan üzerine tweetler attığı tespit edilerek bu kişinin analizi yapılabilir. Örneğin bir kişi 20 tane spor ile alakalı tweet, 5 tane ekonomi , 3 tane siyaset ve 1 tane teknoloji alanında tweet attıysa, algoritma atılan bütün tweetleri sınıflandırır ve bu kişi spor alanına daha ilgili bir kişi diyebilir. Bu sayede bu kişinin spor alanına ilgili olduğu öğrenmiş olunur ve karşısına spor ile alakalı gönderiler veya reklamlar çıkartılabilir.  

<br/>

# VERİSETİNİN OLUŞTURULMASI

<br/>

Dataseti twitterdan çekilen ve istenilen kategorilerde atılmış tweetlerden oluşacaktır. Seçilen kategoriler Spor, Ekonomi, Siyaset, Teknoloji & Bilim ' dir. Bu kategorilerdeki veriler ile model eğitileceği için bu verilerin düzgün veriler olması gerekir. Bu yüzden verilerin çekileceği twitter hesapları düzgün bir şekilde seçilmiştir. Seçilen hesaplarda dikkat edilen özellikler şöyledir:

<br/>
-Hesap aktif olarak paylaşım yapmalı.<br/>
-Yaptığı paylaşımlar sadece o alan ile ilgili olmalı.<br/>
-Günde ortalama 5-10 arası tweet atmalı.<br/>
-Atmış olduğu tweetler metin ağırlıklı olmalı.<br/>


<br/>

Bu kriterleri sağlayan her bir alan için ortalama 8 tane twitter hesabı seçilmiştir. Birden fazla hesap seçilmesinin amacı daha fazla veriye ulaşmaktır. 


<br/>
Pythonda twitterdan istenilen tweetleri çekebilmek için scraping işlemi yapan snscrape pyton kütüphanesi kullanılıyor. <br/>
https://github.com/JustAnotherArchivist/snscrape

<br/>
<br/>

Bu kütüphane verilen sorgu cümlesine göre ve istenilen tweet sayısına göre istenilen tweetleri döndürüyor. Sorgu cümlesinde hesap adı ve istenilen tarih aralığı seçilebilir.<br/><br/> 
### Örnek bir sorgu:<br/><br/>

![ornek_sorgu](https://user-images.githubusercontent.com/77435563/208323507-bd8fee5f-4572-40fe-bb05-75aee43c919e.jpg)

<br/>
Bu sorguda elonmusk isimli kullanıcının 17 aralık 2022 tarihinden önce atmış olduğu tweetler gösteriliyor.

<br/>
<br/>

Datasetini oluştururken yapılan sorgular 2022 yılının tamamı için yapılmıştır. Her farklı kategori için 1 günde 1 hesaptan 16 adet tweet çekilmiştir. Hesaplar gün gün değişmektedir ve eğer 8 hesap varsa 8 gün sonunda aynı hesaptan tekrardan 16 adet tweet çekilmektedir. Verisetinin bu şekilde oluşturulmasının amacı aynı gün ve saatte birden fazla hesaptan aynı tweet gelme ihtimalinin engellenmesidir. 

<br/>

Veriseti oluşturmak için twitterdan her gün bir kategori için 16 adet tweet çekiliyor. 365 ayrı gün için tweet çekildiği için her kategori için 5840 adet tweet bulunmakta.
4 kategorimiz olduğu için verisetinde toplam 23.360 tweet bulunuyor. Modelin başarısını arttırmak için her kategori için eşit miktarda tweet çekiliyor.<br/><br/>
### Verisetinde bulunan kategorilerdeki tweet sayıları:<br/><br/>

![data_set_veri_sayisi](https://user-images.githubusercontent.com/77435563/208323609-097d1ee4-3259-43ca-83ae-c65f41f1a387.jpg)

<br/>
<br/>

4 kategori için 23.360 verinin çekilmesi işlemi ortalama 11 dakika 14 saniye sürüyor.<br/><br/>
### Verilerin çekilme süreleri:<br/><br/>

![Calisma_Suresi](https://user-images.githubusercontent.com/77435563/208323627-4d1c1486-3fd5-4eac-85db-676e4d7ae64f.jpg)

<br/>
<br/>

Verisetindeki kolonlarımız aşağıdaki gibidir:<br/>
-Tweetin atıldığı tarih.<br/>
-Tweeti atan kullanıcının hesap adı.<br/>
-Tweetin kendisi.<br/>
-Tweetin hangi kategoride atıldığı.<br/>

<br/><br/>
Verisetine veriler eklenirken kategorileri ile birlikte ekleniyorlar. Bunun sebebi oluşturulacak olan modeli eğitmek için hangi kategoriye ait olduğunu bilmemiz gerektiğidir. <br/><br/>

### Oluşturulmuş olan verisetinin görseli:<br/><br/>
![data_set](https://user-images.githubusercontent.com/77435563/208323700-beb37519-6467-4230-b2e3-b59df79e17e8.jpg)
