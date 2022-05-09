# Keras

Keras kütüphanesi ile görüntü sınıflandırma işlemlerini yapmak için kullanılan bazı methodlar aşağıda açıklanmıştır. Her başlık bir metod, sınıf vb. durumları ifade etmektedir. Başlıkların altında o durumla ilgili gerekli bilgiler verilmiştir.

## Sequential model : 
Tek input katmanı var. Kolay ama esnek değil.  
## Functional model : 
Birden fazla input alabilir. Biraz daha zor ama esnektir.

## tf.keras.preprocessing.image.ImageDataGenerator
Hem veri arttırma işlemi yapabiliyoruz hemde işlemeye hazır veri elde ediyoruz. Baya kolaylık sağlıyor. 
[Data Augmentation örnekleri için göz atın...](https://github.com/yasinsahin0/plane_cnn_image_classification/tree/main/images/doc_dataAug)  

**featurewise_center=False,**  
**samplewise_center=False,**  
**featurewise_std_normalization=False,**  
**samplewise_std_normalization=False,**  
**zca_whitening=False,**  
**zca_epsilon=1e-06,**  
**rotation_range=0,** :
Görüntüyü kendi ekseninde döndürür.  
**width_shift_range=0.0,** :
Görüntüyü yatay eksende kaydırma işlemi yapar. Görüntü boyutunda değişiklik olmaz.   
**height_shift_range=0.0,** :
Görüntüyü dikey eksende kaydırma işlemi yapar. Görüntü boyutunda değişiklik olmaz.  
**brightness_range=None,** :
Görüntü parlaklığını ayarlar. Parametre tuple türünde float değer alıyor. Örn; (3.0, 4.0)  
**shear_range=0.0,**  
**zoom_range=0.0,** :
Görüntüyü yatay ve dikey olarak zoom yapıyor. örn; 0.4  
**channel_shift_range=0.0,**  
**fill_mode='nearest',** :
{"constant", "nearest", "reflect" or "wrap"}. parametreleri alır.  
**cval=0.0,**  
**horizontal_flip=False,** :
Görüntüyü yatay eksende aynalama işlemi yapar.(True)  
**vertical_flip=False,** :
Görüntüyü dikey eksende aynalama işlemi yapar.(True)  
**rescale=None,** :
Ölçeklendirme yapıyoruz piksel değerleri üzerinde. 0-1 arasına sıkıştırmamızın sebebi bit boyutu yani modele vereceğimiz görüntünün yüksek sayısal değerlerle uğraşmamsını istiyoruz. örn; (rescale=1./255)  
**preprocessing_function=None,**  
**data_format=None,**  
**validation_split=0.0,** :
Doğrulama için ayrılan görüntülerin oranını giriyoruz. yaptığımız değişikliklerin ne kadar gerçekleştiğini kendisi test ediyor. 0 ile 1 arasında float değer alıyor.  
**dtype=None**  


## flow_from_directory

#### directory,                
Veri setimizin bulunduğu main klasör yolunu verdiğimiz parametredir. Veri setinin bulunduğu ana klasör hiyerarşisi aşağıda verildiği gibi ise otomatik olarak sınıflar ayrılacaktır. Eğer tek klasör altında bulunuyorsa bunun için ek metodlar yazmak gereklidir.
* planes
    1. drone
    2. aircraft
    3. helicopter
    4. ....
  
#### target_size=(256, 256),   
Veri setimizdeki görseller farklı boyutlarda olabilir. Bu işlem ile bütün veri setimizi belirlediğimiz boyutlarda yeniden boyutlayarak işlemlere devam edebiliriz. Default olarak 256,256 dır. Aldığı parametre tuple türünde ve int tipinde x ve y değerleridir. x ve y değerleri eşit ise direk int olarak verilebilir.
#### color_mode='rgb',
"grayscale", "rgb", "rgba" 1,3,4 kanal 
#### classes=None**,             
sınıflarımızın isimleri, girilmezse default dizinden alıyor. örn ["drone","airplane"]
#### class_mode='categorical', 
category 2D , binart 1D binary dir.
#### batch_size=32,            
veri grup boyutu, genellikle 2 ve 2** olarak tanımlanır.
#### shuffle=True,             
veri karıştırma işlemi, önerilen True
#### seed=None,
#### save_to_dir=None,         
veri kaydetme
#### save_prefix='',           
#### save_format='png',        
#### follow_links=False,     
#### subset=None,              
"training", "validation" 
#### interpolation='nearest' 
"nearest", "bilinear", "bicubic" PIL >> "lanczos", "box", "hamming" 

## tf.keras.layers.Conv2D(
#### filters,       
(n,n) giriş için (n * n * 3 < filtre sayısı) tavsiye edilir. Görüntü karmaşıklığı ile doğru orantılıdır.
#### kernel_size,
Evrişim matrisi, tuple (int,int) olarak tanımlanır. 
Tek sayı olmalıdır. 1x1,3x3,5x5,7x7 , genellikle 128x128 matris büyüklüğüne sahip görüntülerde 1x1 kullanılır. daha büyük giriş resimlerinde özellik öğrenmeyi genişletmek için 3x3 ve daha büyük kernel kullanılır.
#### strides=(1, 1),
adım kaydırma
#### padding='valid',
pading same ve valid parametresi alıyor. stride 1 ve padding same ise girdi boyutla çıktı boyut aynı oluyor.
#### data_format=None,
#### dilation_rate=(1, 1),
#### groups=1,
#### activation=None,
* Sigmoid : x -2 ile +2 arasında iken y değerleri hızlı bir şekilde değişiyor. İyi bir sınıflayıcı olarak kullanılabilir. +sonsuz, -sonsuz arasında değer alırken 0,1 arasında çıkış üretir. Bu iyi haber aktivasyon değerleri çok yükselmez. Fonksiyon uç noktaları değişimlere az tepki gösteriyor buda eksi bir durum. Bu noktalarda değer 0 a çok yaklaştığı için gradyan ölmesi problemi (vanishing gradient) doğurur. Öğrenme çok çok az gerçekleşir buda istemediğimiz bir durum :)  
* Hiperbolik tanjant : Sigmoid fonksiyona benzemektedir lakin fonksiyon aralığı (-1,+1) arasındadır. Türevi daha dik olması daha fazla değer alabileceği anlamına gelmektedir. Fakat bu fonksiyonunda uç noktalarında gradyan ölmesi durumu vardır.
* ReLu : Eksi bölgelerde sıfır değeri alması ağın daha hızlı çalışacağı anlamına gelmektedir. Çok fazla nöronlu sinir ağlarında yaygın kullanılır. Verimliliği yüksektir. Eksi bölgede türevininde sıfır olması öğrenmenin gerçekleşmeyeceği anlamına geliyor buda üzücü tabi :)
* Leaky ReLU : Sızıntı değeri 0,01 olarak veriliyor. Tanım aralığı - sonsuza doğru gidiyor. - bölgede değerler 0 olmadığı için öğrenme devam ediyor. gradyan ölmesi durumu yaşanmıyor.
* softmax : Sigmoid fonksiyonuna benzer yapıdadır. Sınıflayıcı olarak kullanıldığında iyi performans gösterir. İkiden fazla sınıf olduğu durumlarda modelin çıkış katmanında tercih edilir. Girdinin belirli sınıfa ait olma olasılığını 0 ile 1 arasında değerler üreterek belirlenmesini sağlar. Olasılıksal bir yorumlama gerçekleştirir.
#### use_bias=True,
#### kernel_initializer='glorot_uniform',
#### bias_initializer='zeros',
#### kernel_regularizer=None,
#### bias_regularizer=None,
#### activity_regularizer=None,
#### kernel_constraint=None,
#### bias_constraint=None,

## Kaynaklar
* https://www.tensorflow.org/api_docs/python/tf/keras/preprocessing/image/ImageDataGenerator
* https://www.tensorflow.org/api_docs/python/tf/keras/layers/Conv2D
* https://www.tensorflow.org/api_docs/python/tf/keras/activations
* https://pyimagesearch.com/2018/12/31/keras-conv2d-and-convolutional-layers/
* https://ayyucekizrak.medium.com/derin-%C3%B6%C4%9Frenme-i%C3%A7in-aktivasyon-fonksiyonlar%C4%B1n%C4%B1n-kar%C5%9F%C4%B1la%C5%9Ft%C4%B1r%C4%B1lmas%C4%B1-cee17fd1d9cd
* 