# Docker - 1: ``Docker Nedir? Docker’a Giriş ve Temel Kavramlar”

## 1.1 Docker

**Docker**, yazılım uygulamalarının geliştirilmesi, dağıtılması ve çalıştırılması için kullanılan **açık kaynaklı** bir platformdur. Basit anlamda, uygulamalarınızı ve bunların tüm bağımlılıklarını (kütüphaneler, konfigürasyonlar vb.) bir **paket** halinde birleştirerek, farklı ortamlarda (geliştirme, test, üretim) aynı şekilde çalışmasını sağlar.

Bu sayede ``*Localde (bende) çalışıyor ama başka birinde neden çalışmıyor?*” gibi sorunlarla karşılaşma olasılığınızı büyük ölçüde azaltır.

## 1.2 Docker’ın Ortaya Çıkışı ve Önemi

Docker’dan önce de konteynerleşme kavramı mevcuttu. Özellikle Linux işletim sisteminde çalışnan **LXC(Linux Containers)** gibi teknolojiler, uygulamaları izole ortamlarda çalıştırmak için kullanılıyordu. Ancak bu teknolojiler, karmaşık yapıları ve kullanım zorlukları nedeniyle yaygınlaşmakta zorlanıyordu.

2013 yılında Solomon Hykes liderliğindeki bir ekip tarafından geliştirilen Docker, LXC gibi teknolojilerin üzerine inşa edilerek,  konteynerleşmeyi daha basit daha kullanışlı ve daha erişilebilir hale getirdi. Docker’ın en büyük yeniliklerinden biri, konteynerleri oluşturmak ve yöntemek için daha kullanıcı dostu bir arayüz sunmasıydı.

Docker’ın başarısının nedenleri ve önemi:

- **Tutarlılık**
    
    Uygulamalarınızı her yerde aynı şekilde çalıştırarak, geliştirme ile üretim arasındaki farkları ve tutarsızlıkları ortadan kaldırır.
    
- **İzolasyon**
    
    Her uygulama kendi bağımsız ortamında çalıştığı için, bir uygulamanın çökmesi diğerini etkilemez.
    
- **Verimlilik**
    
    Kaynakları daha etkin kullanarak, aynı donanım üzerinde daha fazla uygulama çalıştırma olanağı sağlar.
    
- **Hızlı Dağıtım**
    
    Uygulamaları hızlıca oluşturup dağıtmanıza yardımcı olur.
    
- **Ölçeklenebilirlik**
    
    Yükte artış olduğunda, **konteyner** sayısına kolayca arttırarak daha verimli kullanım sunar.
    

Docker‘ın sayesinde:

- **Mikroservis miamarisi** daha popüler hale geldi.
- **DevOps** kültürünün benimsenmesi hızlandı.
- **Bulut bilişim** teknolojileriyle daha kolay entegrasyon sağlandı.
- **Uygulamaların daha hızlı ve güvenli bir şekilde dağıtımı** mümkün oldu.

## 1.3 Docker Temel Kavramları

1. **Container**
    1. ***Tanım:*** Bir konteyner, uygulamanızın tüm bağımlılıklarıyla birlikte paketlendiği bir izole ortamdır.
    2. ***İşlev:*** Uygulamanızın her yerde aynı şekilde çalışmasını sağlar. İşletim sistemi çekirdeğini paylaşırken, diğer uygulamalardan izole bir ortam sunar.
    
2. **Image**
    1. ***Tanım:*** Bir konteynerin okunabilir bir şablonudur. İçerisinde uygulamanızın kodları, konfigürasyonları ve bağımlılıkları bulunur.
    2. ***İşlev:*** Yeni konteynerler oluşturmak için kullanılır. Bir kez oluşturulduktan sonra değiştirilemez ancak yeni br Image’ye (görüntüye) kopyalanarak üzerinde değişiklik yapabilir.
    
3. **Container Registry**
    1. ***Tanım:*** Oluşturduğunuz Image’lerin (görüntülerin) depolandığı merkezi bir depolama alanıdır.
    2. ***İşlev:*** Image’leri (görüntüleri) farklı ekiplerle paylaşmanıza, versiyonlamanıza ve yönetmenize olanak tanır.
    
4. **Docker File**
    1. ***Tanım:*** Bir Image’ı (görüntüyü) nasıl oluşturacağınızı tanımlayan bir metin dosyasıdır.
    2. ***İşlev:*** Bir taban görüntüsünü seçerek, gerekli yazılımları yükleyerek ve uygulamanızın kodlarını kopylalayarak bir Image (görüntü) oluşturur.
    
5. **Docker Compose**
    1. ***Tanım:*** Birden fazla Container’ı (Konteyneri) yöneten bir araçtır.
    2. ***İşlev:*** Bir projedeki tüm hizmetleri tek bir komutla başlatıp durdurmanıza olanak tanır.
    
6. **Docker Swarm**
    1. ***Tanım:*** Birden fazla Docker motoru üzerinde çalışan Contaier’ları (konteynerleri) yönetmek için kullanılan bir kümeleme çözümüdür.
    2. ***İşlev:*** Büyük ölçekli uygulamaları dağıtmak ve yönetmek için kullanılır.

## 1.4 Docker Kurulumu

- Docker’ın resmi web sitesinden kendi bilgisayarınızın işletim sistemine uygun olanını indirin.
- İndirme işelemi tamamlandıktan sonra, Docker’ı yüklemek için adımlar geçin ve yükleyin.
- Yükleme işlemi tamamlandıktan sonra, Docker’ çalıştırmak için komut istemini veya powershell’ i açın.
- Docker’ı yükleme işlemi tamamlandığını ve docker kullanıma hazır olduğunu kontrol etmek için `docker version` komutunu girin.

## 1.5 Docker ve Sanallaştırma

**Sanallaştırma**, fiziksel olarak bir bilgisayarın kaynaklarını (CPU, bellek, disk, ağ vb.) birden fazla bağımsız sanal makineye (Virtual Machine) bölen bir teknolojidir. Bu sayede, tek bir fiziksel sunucu üzerinde farklı işletim sistemleri ve uygulamaları aynı anda çalıştırılabilir.

### 1.5.1 Sanallaştırmanın Önemi:

- Çoklu İşletim Sistemi Kullanımı:
    
    Tek bir bilgisayarda birden fazla işletim sistemi kullanmanıza olanak tanır.
    
- Uygulama İzolasyonu:
    
    Farklı uygulamaları birbirinden izole ederek çakışma riskini azaltır.
    
- Test Ortamları:
    
    Yeni yazılımlar veya güncellemeleri sanal ortamlarda test etme imkanı sunar.
    
- Kaynak Verimliliği
    
    Donanım kaynaklarını daha etkin kullanmanıza yardımcı olur.
    

### 1.5.2 Sanallaştırmayı Etkinleştirme:

Sanallaştırmayı etkinleştirmek için öncelikle bilgisayarınızın donanımının bu özelliği desteklediğinden emin olmanız gerekir. Genellikle modern işlemciler sanallaştırmayı destekler.

- BIOS/UEFI Ayarlarını Kontrol Etme:
    - Bilgisayarınızı yeniden başlatırken genellikle F2, F10 veya Del tuşlarına basarak *BIOS/UEFI* ayarlarına girebilirsiniz.
    - "Virtualization" veya “Intel VT-x/AMD-v" gibi bir seçenek arayın ve bu seçeneği etkinleştirin.
    - Değişiklikleri kaydedip bilgisayarınızı yeniden başlatın.
- Windows Özelliklerini Etkinleştir:
    - Windows 10:
        - Başlat menüsünde "Windows özellikleri" yazın ve açılan sonuçtan "Windows özelliklerini aç veya kapat"ı seçin.
        - "Hyper-V" seçeneğini işaretleyin ve Tamam'a tıklayın.
        - Bilgisayarınızı yeniden başlatın.
    - Windows 11:
        - Başlat menüsünde aşağıdaki yolu takip ediniz.
        - “Hyper -V” seçeneğini etkinleştirin.
        
        ```mermaid
        graph
          Başlat --> Ayarlar--> Uygulamalar --> Özellikler --> Windows'un_isteğe_bağlı_özellikleri --> Hyper-V
        ```
        

- Sanallaştırmanın Etkin Olup Olmadığını Kontrol Etme:
    - Görev Yöneticisi:
        - Görev Yöneticisini açın (Ctrl+Shift+Esc).
        - Performans sekmesine gidin ve CPU bölümünde sanallaştırma ile ilgili bir bilgi olup olmadığını kontrol edin.
    - Komut İstemi:
        - Komut istemini açin (cmd) ve `systeminfo` komutunu çalıştırın. Çıktıda sanallaştırma ile ilgili bilgiler yer alacaktır.