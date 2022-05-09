# Keras

Keras kütüphanesi ile görüntü sınıflandırma işlemlerini yapmak için kullanılan bazı methodlar aşağıda açıklanmıştır. Her başlık bir metod, sınıf vb. durumları ifade etmektedir. Başlıkların altında o durumla ilgili gerekli bilgiler verilmiştir.

## Sequential model : 
Tek input katmanı var. Kolay ama esnek değil.  
## Functional model : 
Birden fazla input alabilir. Biraz daha zor ama esnektir.

## tf.keras.preprocessing.image.ImageDataGenerator

#### featurewise_center=False,
#### samplewise_center=False,
#### featurewise_std_normalization=False,
#### samplewise_std_normalization=False,
#### zca_whitening=False,
#### zca_epsilon=1e-06,
#### rotation_range=0,
#### width_shift_range=0.0,
#### height_shift_range=0.0,
#### brightness_range=None,
#### shear_range=0.0,
#### zoom_range=0.0,
#### channel_shift_range=0.0,
#### fill_mode='nearest',
#### cval=0.0,
#### horizontal_flip=False,
#### vertical_flip=False,
#### rescale=None,
#### preprocessing_function=None,
#### data_format=None,
#### validation_split=0.0,
#### dtype=None


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
aktivasyon fonksiyonları
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