# Miuul Git & GitHub Kapsamlı Kurs Notları

Bu rehber, Miuul Git & GitHub eğitimi boyunca öğrenilen temel kavramları, terminal komutlarını, branch yönetimini ve ileri seviye Git araçlarını içermektedir.

---

## 1. Temel Kavramlar ve Yapılandırma

**Versiyon Kontrol Sistemleri**

- **DVCS (Distributed VCS):** Dağıtık sistemdir. Her geliştirici projenin tam bir kopyasını kendi yerelinde taşır (Örn: Git).
- **CVCS (Centralized VCS):** Merkezi sistemdir. Değişiklikler tek bir ana sunucu üzerinden yönetilir (Örn: SVN).

**Sistem ve Kimlik Ayarları**

```bash
# Kullanıcı bilgileri tanımlama
git config --global user.name "kendi_adin"
git config --global user.email "kendi_emailin"

# Renkli terminal çıktısını aktifleştirme
git config --global color.ui true

# Mevcut tüm ayarları listeleme ve kontrol etme
git config --global user.name
git config --global user.email
git config --list
```

# SSH (Secure Shell) Bağlantısı

Ağ üzerinde güvenli iletişim sağlayan protokoldür.

Private Key (Özel Anahtar): Bilgisayarda saklanır, paylaşılmaz (veri çözümleme).

Public Key (Genel Anahtar): GitHub'a eklenir (veri şifreleme).

2. Temel Git Komutları ve Çalışma Akışı
   Depo Oluşturma ve Takip

```
git init # Bulunulan dizinde yeni Git deposu başlatır
git status # Dosyaların mevcut durumunu gösterir
git add . # Tüm değişiklikleri sahneye (Staging Area) ekler
git add dosya.txt # Belirli bir dosyayı sahneye ekler
```

# Commit (Kaydetme) İşlemleri

```
git commit -m "Mesaj" # Yapılan değişiklikleri mesajla kaydeder
git log # Geçmiş commit kayıtlarını listeler
git commit --amend # Son atılan commit'i düzenler veya yeni dosyaları son commit'e ekler
```

# Kısayollar (Alias) ve Geçici Depolama (Stash)

## Gelişmiş log görünümü için alias tanımlama

```
git config --global alias.takmaad "log --all --graph --decorate --oneline"
```

# Tamamlanmamış değişiklikleri geçici olarak kaldırma

```
git stash
```

# Temizlik ve İnceleme Komutları

\*gitk: Grafiksel Git arayüzünü açar.

\*git gc: Gereksiz verileri temizler ve depoyu optimize eder.

\*git fsck: Bozuk veya yetim kalmış dosyaları kontrol eder.

\*git rm dosya.txt: Dosyayı hem çalışma dizininden hem de Git takibinden siler.

\*git diff: İki dosya veya commit arasındaki farkları gösterir.

\*git show: Belirtilen commit'in detaylarını görüntüler.

3. Uzak Depo (Remote) Yönetimi

```
git clone <URL> # Uzak depoyu bilgisayara kopyalar
git remote add origin <URL> # Yerel depoyu uzak depoya bağlar
git remote -v # Bağlı uzak depoları detaylı listeler
git remote rename eski_ad yeni_ad # Uzak depo adını değiştirir
git remote remove uzak_adi # Uzak depo bağlantısını siler
git remote get-url uzak_adi # Uzak deponun URL adresini görüntüler
git remote set-url uzak_adi yeni_url # Uzak depo URL adresini günceller
```

# Veri Transferi

```
git push -u origin main # Yereldeki commit'leri uzak depoya gönderir
git fetch # Uzak depodaki güncellemeleri kontrol eder (yerelle birleştirmez)
git pull # Uzak depodaki değişiklikleri çeker ve yerelle birleştirir
```

4. Branch (Dal) Yönetimi ve Switch

```
git branch # Mevcut dalları listeler
git branch frontend # 'frontend' adında yeni dal oluşturur
git checkout frontend # 'frontend' dalına geçiş yapar
git switch frontend # Dal değiştirmek için modern alternatif
git switch -c yenidal # Yeni dal oluşturur ve doğrudan o dala geçer
git branch -D dal_adi # Belirtilen dalı zorla siler
```

5. Merge (Birleştirme) Stratejileri
   Fast-Forward Merge: Çakışma yoksa dalı doğrudan ana dalın önüne taşır (git merge feature).

No-Fast-Forward (--no-ff): Dalları birleştirirken geçmişin korunması için zorunlu olarak yeni bir merge commit'i oluşturur (git merge --no-ff feature).

Squash Merge: Yan daldaki tüm commit'leri tek bir commit haline getirerek ana dala ekler (git merge --squash feature).

Octopus Merge: Birden fazla dalı aynı anda ana dala birleştirmek için kullanılır (git merge branch1 branch2 branch3).

6. Merge vs Rebase

Özellik,Merge,Rebase
-Commit Oluşumu,Yeni bir Merge Commit oluşturur.,"Ekstra commit oluşturmaz, geçmişi düzleştirir."

-Geçmiş Sırası,Commit tarihlerini ve dalların orijinal sırasını korur.,Commit'leri hedef dalın ucuna yeniden yazar.

-Güvenlik,"Güvenlidir, geçmişi değiştirmez.","Dikkat gerektirir, ortak dallarda geçmişi değiştirmek risklidir."
-Kullanım,

```
git merge branch_adi
```

```
git checkout featuregit rebase master
```

7. Gelişmiş Git Araçları
   Git Tag (Etiketleme)
   Sürümleri veya önemli commit'leri işaretlemek için kullanılır.

git tag -a v1.0 -m "Sürüm 1.0 yayınlandı"

Git Grep (Arama)
Proje içinde metin tabanlı arama yapar.

```
git grep "hello world" # Tüm projede arar
git grep "hello world" -- .txt # Sadece .txt dosyalarında arar
git grep "hello world" -- src/ # Sadece src/ dizininde arar
```

# Git Reset (Geri Alma)

-Soft Reset (git reset HEAD~1): Commit'i iptal eder, değişiklikleri sahnede (staging) tutar.

-Mixed Reset (git reset veya git reset dosya.txt): Commit ve sahneleme durumunu iptal eder, dosyaları korur.

-Hard Reset (git reset --hard): Belirtilen noktadan sonraki tüm değişiklikleri ve dosyaları kalıcı olarak siler.

# Git Conflict (Çakışma Yönetimi)

-Aynı dosyanın aynı satırında farklı değişiklikler yapıldığında ortaya çıkar. Çakışan dosyalar elle düzenlendikten sonra git add . ve git commit adımları izlenerek çözülür.
