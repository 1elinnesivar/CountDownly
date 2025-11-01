# GitHub'a Yükleme Talimatları

## Adım 1: GitHub'da Repository Oluşturun
1. https://github.com adresine gidin ve giriş yapın
2. Sağ üstteki "+" ikonuna tıklayın
3. "New repository" seçeneğini seçin
4. Repository adını girin: `CountDownly` (veya istediğiniz isim)
5. Public veya Private olarak seçin
6. **ÖNEMLİ:** "Initialize this repository with a README" seçeneğini **işaretlemeyin** (zaten README.md dosyamız var)
7. "Create repository" butonuna tıklayın

## Adım 2: Remote Repository Ekleme ve Push

GitHub'da repository oluşturduktan sonra, aşağıdaki komutları sırayla çalıştırın:

```bash
# Remote repository'yi ekleyin (URL'yi kendi GitHub URL'nizle değiştirin)
git remote add origin https://github.com/KULLANICI-ADI/REPO-ADI.git

# Dosyaları GitHub'a yükleyin
git push -u origin main
```

**Not:** `KULLANICI-ADI` ve `REPO-ADI` kısımlarını kendi GitHub kullanıcı adınız ve repository adınızla değiştirin.

## Alternatif: GitHub CLI Kullanımı

Eğer GitHub CLI yüklüyse:
```bash
gh repo create CountDownly --public --source=. --remote=origin --push
```

## Sonraki Adımlar

Push işlemi tamamlandıktan sonra:
- GitHub sayfanızda tüm dosyalarınızı görebilirsiniz
- İsterseniz GitHub Pages ile projeyi canlıya alabilirsiniz (Settings > Pages)
- README.md dosyası otomatik olarak ana sayfada görünecektir

