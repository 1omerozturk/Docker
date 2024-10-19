# Docker - 2: ``Docker Image ve Container'ları Anlamak”

## 2.1 Docker Image

Docker Image, bir uygulamanın çalışması için gerekli tüm dosyaların, kütüphanelerin ve bağımlılıkların tek bir paket halinde toplandığı, okunabilir ancak değiştirilemez (read-only) bir şablondur. Bu sayede, bir uygulama ve tüm bileşenleri, farklı ortamlarda (geliştirme, üretim, test vb.) aynı şekilde çalışıtırılabilir.

### **Katmanlı Yapı:**

![https://images.unsplash.com/photo-1526073733167-1b6d55175336?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1526073733167-1b6d55175336?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

Docker image’ler, birbiri üzerine eklenen katmanlardan (layer) oluşur. Her katman, bir önceki katmana göre yapılan değişiklikleri temsil eder. Bu katmanlı yapı **image’lerin** daha hızlı oluşturulmasını ve daha az yer kaplamasını sağlar. 

Örneğin;

- ***Base image Layer:*** Temel işletim sistemi (Ubuntu, CentOS vb.) içeren ilk katmandır.
- ***Intermediate Layers:*** Uygulamaya özel yazılımların, kütüphanlerin ve konfigürasyonların eklendiği katmanlardır.
- ***Top Layer:*** Son katman, çalıştırılabilir dosyaları ve uygulamanın giriş noktasını içerir.

Bu katmanlı  yapı sayesinde, bir Image’de yapılan küçük bir değişiklik için tüm image’in tekrar oluşturulmasına gerek kalmaz. Sadece değişen katman yeniden oluşturulur ve diğer katmanlar üzerine eklenir.

### **Read-Only Özelliği:**

![https://images.unsplash.com/photo-1602503874881-c97c18856ae6?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1602503874881-c97c18856ae6?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

Docker Image’leri read-only olması, Image’lerin değiştirilmesini ve bozulmasını önler. Bu sayede image’ler güvenli bir şekilde depolanabilir ve dağıtılabilir. Bir image’i çalıştırmak için, image’den bir container oluşturulur. Container, image’in bir kopyasıdır ve üzeirnde değişklikler yapılabilir. Ancak , container üzerinde yapılan değişiklikler, image’i etkilemez.

Örneğin;

- *Base image:* Ubuntu 20.04
- *Image 1:* Nginx web sunucusu
- *Image 2:* PHP uygulaması

Bu üç image’i birleştirerek, PHP uygulamasının Nginx ile çalışan bir web sunucusu üzerinde çalıştırılabileceği bir image oluşturabilir.

### **Union File System’in Çalışma Mantığı:**

![https://images.unsplash.com/photo-1461360228754-6e81c478b882?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1461360228754-6e81c478b882?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

1. Farklı image’lerin katmanları, bir dosya sistemi hiyerarşisi içinde birleştirilir.
2. En üstteki katman, en son yapılan değişiklikleri içerir.
3. Alttaki katmanlar,  daha önceki değişiklikleri içerir.
4. Bir dosya ve dizin istendiğinde, sistem önce en üstteki katmanda arar. Bulunmaması durumunda alt katmanlarda aramaya devam eder.
- **Avantajları:**
    - Hız ve Verimlilik: Sadece değişen katmanlar disk üzerinde tutulur.
    - Esneklik: Farklı image’lerin birleştirilerek yeni image’ler oluşturulabilir.
    - Güvenlik: Image’ler read-only olduğu için, istenmeyen değişiklikler önelenir.
    - Paylaşılabilirlik: Image’ler, Docker registry’lerde depolanarak diğer kullanıcılarla paylaşılabilir.

Sonuç olarak, Docker Image’ler, uygulamaların geliştirilmesi, dağıtılması ve yönetilmesi için güçlü bir araçtır. Katmanlı yapı, read-only özelliği ve Union File System gibi özellikler sayesinde, Docker image’ler, modern yazılım geliştirme süreçlerinde vazgeçilmez bir hale gelmiştir.

## 2.2 Docker Hub ve Image Yönetimi

![https://images.unsplash.com/photo-1523841589119-b55aee0f66e7?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1523841589119-b55aee0f66e7?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

**Docker Hub**, dünyanın en büyük konteyner image deposudur. Burada milyonlarca önceden oluşturulmuş image’leri bulabilir, kendi image’larınızı depolayabilir ve diğer geliştiricilerle paylaşabilirsiniz. Tıpkı Github’ın yazılım projeleri için olduğu gibi, Docker Hub da container dünyasının merkezidi.

### 2.2.1 Docker Hub’dan Image İndirme - (docker pull)

![https://images.unsplash.com/photo-1541742425281-c1d3fc8aff96?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1541742425281-c1d3fc8aff96?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

Bir image’i Docker Hub’dan indirmek için `**docker pull**` komutu kullanılır.

```bash
docker pull <image_name>:<tag>
```

- <image_name>
    
    İndirmek istediğimiz image’in adı.
    
    Örneğin; (ubuntu, nginx, python).
    
- <tag>
    
    Image’in sürümünü belirten etiket veya sürüm adı.
    
    Örneğin; (latest, 20.04, 3.9).
    

> Örnek
> 

```bash
docker pull ubuntu:20.04
```

- Bu komut, Ubuntu 20.04 işletim sistemini içeren bir image indirir.

### 2.2.2 Docker Hub’a Kendi Image’imizi Push Etme - (docker-push)

![https://images.unsplash.com/photo-1632298095711-d546888879ee?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1632298095711-d546888879ee?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

Kendi oluşturduğumuz bir image’i [Docker Hub](https://www.docker.com/products/docker-hub/)’a yüklemek için **`docker push`** komutunu kullanırız.

Docker hesabınızın olduğunu varsayarak bir repository oluşturmanız gerekir.

```bash
docker push <user_name>/<repository>:<tag>
```

- <user_name>
    
    Docker Hub kullanıcı adınız.
    
- <repository>
    
    Oluşturduğunuz respository’nin adı.
    
- <tag>
    
    Image’in sürümünü belirten etiket.
    

> Örnek
> 

```bash
docker push myuser/myimage:v1
```

- Bu komut “myuser” adlı kullanıcının “myimage” adlı repository’sine “V1” etiketli bir image yükler.

Not: Docker Hub’a image push etmek için yerel makinenizdeki image’in adı ile Docker Hub’daki repository adı ve etiketi aynı olmalıdır.

### 2.2.3 Özel Image Repository’lerinin Kullanımı ve Yönetimi

Docker Hub dışında da özel image repository’leri oluşturabilirsiniz. Bu, kurumsal ortamlarda veya daha fazla kontrol isteyen durumlarda tercih edilir. Bazı popüler özel registry’ler arasında ***Google Contaier Registry***, ***Amazon ECR*** ve ***Azure Container Registry*** bulunur.

**Özel registry’lerin avantajları:**

- Güvenlik:
    
    Kurumsal ağınız içinde daha iyi kontrol ve güvenlik sağlar.
    
- Özelleştirme:
    
    Kendi ihitiyaçlarınıza göre özelleştirebilirsiniz.
    
    Örneğin; kimlik doğrulama, erişim kontrolü
    
- Ölçeklenebilirlik:
    
    Büyük ölçekli prtojeler için daha iyi ölçeklenebilirlik sunar.
    

Özel Registry Kullanımı:

1. Registry’i yapılandırma: Registry’i kurmak veya bulut sağlayıcının sunduğu hizmeti kullanmak.
2. Kimlik doğrulama: Registry’e erişmek için doğru kimlik bilgilerini kulalnmak.
3. Image push/pull: **`docker push`**  ve **`docker pull`** komutlarını kullanarak image’leri göndermek ve almak.

 

> Örnek
> 

```bash
# Docker'ı Google Cloud ile bağlama
gcloud auth configure-docker

# Image push
docker tag myimage gcr.io/<project_id>/myimage:v1
docker push gcr.io/<proje_id>/myimage:v1
```

Docker Hub, container image’lerı için merkezi bir depolama ve paylaşım platformudur. Kendi image’larınızı oluşturabilir, Docker Hub’dan başkalarının oluşturduğu image’ları indirebilir ve özel registry’ler kullanarak daha fazla kontrol ve güvenlik sağlayabilirsiniz.

## 2.3 Docker Container

![https://images.unsplash.com/photo-1493946740644-2d8a1f1a6aff?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1493946740644-2d8a1f1a6aff?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

Tekrar hatırlatmak gerekirse Docker Container, bir uygulamanın ve tüm bağımlılıklarının (kütüphaneler, konfigürasyonlar vb.) paketlenmiş bir halidir. Bu paket, herhangi bir altyapıda tutarlı bir şekilde çalıştırılabilen, hafif ve izole edilmiş bir ortam sağlar. Container’ler, sanal makinelere göre daha hızlı başlatılır, daha az kaynak tüketir ve daha kolay yönetilir.

### 2.3.1 Container ve Image İlişkisi

- **Image:** Bir container’ın şablonu gibidir. Okunabilir ve değiştirilemez bir dosyadır. Bir image, bir işletim sisteminin temel katmanları,  uygulamaları ve konfigürasyonları içerir.
- **Container:** Bir image’dan oluşturulan çalıştırılabilir bir örnektir. Image’deki talimatlara göre başlatılır ve çalışır. Birçok container, aynı image’dan oluşturulabilir.

> Örnek
> 

<aside>
💡

Bir Ubuntu işletim sistemine sahip ve üzerinde Nginx web sunucusunun kurulu olduğu bir image düşünelim. Bu image’dan birden fazla container oluşturulabiliriz. Her container, aynı image’dan gelmesine rağmen farklı bir IP adresine sahip olabilir ve farklı konfigürasyonlarla çalışabilir.

</aside>

### 2.3.2 Container’ların İzole Edilmesi

Container’ler birbirlerinden ve ana makineden izole edilerek güvenlik ve kanyak paylaşımı konularında avantaj sağlar. Bu izolasyon, **namespace** ve **cgrups** mekanizmalarıyla sağlanır.

- **Namespace**
    
    Bir container’ın görebileceği ve erişebileceği kaynakları sınırlar. Her container, kendi ağ, PID (Procces ID), mount noktaları, kullanıcı ve diğer namespace’lere sahiptir. Bu sayede, bir container’da meydana gelen bir hata diğer container’ları etkilemez.
    
- **Cgroups**
    
    Bir container’ın kullanabileceği sistem kaynaklarını (CPU, bellek, disk, ağ) sınırlar ve izler.
    
    Bu sayede, bir container diğer container’ların kaynaklarını tüketemez ve sistem kaynakları daha etkin bir şekilde kullanılır.
    

**Özetle**

- Docker Image: Okunabilir, değiştirilemez ve container’ların şablonu olan bir dosyadır.
- Docker Container: Bir image’dan oluşturulan, çalıştırılabilir ve izole edilmiş bir ortam sağlar.
- Namespace: Container’ların görebileceği ve erişebileceği kaynakları sınırlar.
- Cgroups: Container’ların kullanabileceği sistem kaynaklarını sınırlar ve izler.

### 2.3.3 Docker Container Kullanım Alanları

### Mikroservis Mimarileri

Uygulamaların küçük, bağımsız hizmetlere ayırmak için.

### DevOps

CI/CD (Sürekli entegrasyon ve sürekli dağıtım) süreçlerini otomatikleştirmek için.

### Bulut Bilişim

Bulut platformlarında uygulamaları dağıtmak için.

### Web Uygulamaları

Web uygulamalarını hızlı ve güvenli bir şekilde dağıtmak için.

- **Ek Anahtar Kelimeler**
    - **Dockerfile:** Bir image’ı nasıl oluşturacağımızı tanımlayan bir dosyadır.
    - **Docker Compose:** Birden fazla container’ı yönetebilmek için kullanılan bir araçtır.
    - **Kubernets:** Büyük ölçekli container orchestration platformudur.

## 2.4 Container Yönetim Komutları ve Yaşam Döngüsü

![https://images.unsplash.com/photo-1494961104209-3c223057bd26?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1494961104209-3c223057bd26?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

### 2.4.1 Temel Docker komutları

![https://images.unsplash.com/photo-1592991538534-00972b6f59ab?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1592991538534-00972b6f59ab?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

- **`docker ps`**  ⇒ Çalışmakta olan container’ları listeler.
    - **`-a`**  ⇒ tüm container’ları (çalışan, durdurulmuş, silinmiş) listelemek için kullanılır.
- **`docker run`**   ⇒ Yeni bir container oluşturur ve çalıştırır.
    - **`-d`**  ⇒ Container’ı arka planda çalıştırmak için kullanılır.
    - **`-p`**  ⇒ Container’ın portunu ana makinenin bir portuna eşlemek için kullanılır.
    - **`-v`**  ⇒ Ana makinenin bir dizinini container’ın bir dizinine bağlamak için kullanılr.
- **`docker start`**  ⇒ Oluşturulan bir Container’ı çalıştırır.
- **`docker exec`**  ⇒ Çalışan bir container’ın içinde komut çalıştırır.
- **`docker stop`**  ⇒ Çalışan bir container’ı durdurur.
- **`docker rm`**  ⇒ Durdurulmuş bir container’ı siler.

### **2.4.2 Diğer Önemli Komutlar**

![https://images.unsplash.com/photo-1524741978410-350ba91a70d7?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1524741978410-350ba91a70d7?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

- **`docker images`**  → Yerel olarak kaydedilmiş image’ları listeler.
- **`docker pull`**  → Bir image’ı Docker Hub veya başka bir registry’den çeker.
- **`docker push`**  → Yerel bir image’ı Docker Hub veya başka bir registry’e gönderir.
- **`docker build`**  → Bir Dockerfile’dan bir image oluşturur.
- **`docker commit`**  → Çalışan bir container’dan yeni bir image oluşturur.

### 2.4.3 Container Yaşam Döngüsü

![https://images.unsplash.com/photo-1527266237111-a4989d028b4b?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1527266237111-a4989d028b4b?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

1. **Oluşturma: `docker run`**  komutu ile bir image’dan yeni container oluşturulur.
2. **Çalıştırma:** Oluşturulan container, **`docker start`**  komutu ile çalıştırılır.
3. **Durdurma:** Çalışan bir container, **`docker stop`**  komutu ile durdurulur.
4. **Silme:** Durdurulmuş bir container, **`docker rm`**  komutu ile silinir.

### 2.4.4 Loglara Erişim

![https://images.unsplash.com/photo-1715079029357-1a74c8c5eae2?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb](https://images.unsplash.com/photo-1715079029357-1a74c8c5eae2?ixlib=rb-4.0.3&q=85&fm=jpg&crop=entropy&cs=srgb)

- **`docker logs`**  ⇒ Bir container’ın tüm loglarını görüntüler.
    - **`-f`**  ⇒ Logları gerçek zamanlı olarak takip etmek için kullanılır.

### 2.4.5 Örnek Kullanımlar

- Bir Nginx container’ı oluşturup çalıştırmak
    
    ```bash
    docker run -d -p 80:80 nginx
    ```
    
- Çalışan bir container içinde bir komut çalıştırmak
    
    ```bash
    docker exec my_container bash
    ```
    
- Bir container’in loglarını görüntülemek
    
    ```bash
    docker logs -f my_container
    ```