# Paddle Ödeme Entegrasyonu Kurulum Rehberi

Bu dosya, CountDownly projesine Paddle ödeme entegrasyonunu kurmanız için adım adım talimatlar içerir.

## Adım 1: Paddle Hesabı Oluşturun

1. https://vendors.paddle.com adresine gidin
2. "Sign Up" ile yeni hesap oluşturun veya mevcut hesabınızla giriş yapın
3. Hesabınızı doğrulayın (e-posta, telefon, vb.)

## Adım 2: Vendor ID'nizi Bulun

1. Paddle Dashboard'a giriş yapın
2. Sol menüden **Settings** > **Account** bölümüne gidin
3. **Vendor ID** değerinizi kopyalayın (örn: `12345`)

## Adım 3: Ürün ve Fiyat Oluşturun

1. Sol menüden **Catalog** > **Products** bölümüne gidin
2. **"Add product"** butonuna tıklayın
3. Ürün bilgilerini doldurun:
   - **Product name**: CountDownly Premium
   - **Description**: Unlimited countdown timer generator subscription
   - **Type**: Subscription (Recurring)
4. **Pricing** bölümünde:
   - **Price**: $10.00
   - **Billing cycle**: Monthly
   - **Currency**: USD
5. Ürünü kaydedin
6. Oluşturduğunuz ürünün **Price ID**'sini kopyalayın (örn: `pri_01xxxxx...`)

## Adım 4: Sandbox/Test Modunu Ayarlayın

1. Paddle Dashboard'da **Settings** > **Environment** bölümüne gidin
2. **Sandbox** modunu aktif edin (test ödemeleri için)
3. Test kartı bilgileri:
   - **Card number**: `4242 4242 4242 4242`
   - **Expiry date**: Herhangi bir gelecek tarih (örn: `12/25`)
   - **CVV**: Herhangi bir 3 haneli sayı (örn: `123`)
   - **ZIP code**: Herhangi bir ZIP kodu (örn: `12345`)

## Adım 5: index.html Dosyasını Yapılandırın

`index.html` dosyasını açın ve aşağıdaki satırları bulun:

```javascript
const PADDLE_VENDOR_ID = 'YOUR_PADDLE_VENDOR_ID';
const PADDLE_PRICE_ID = 'pri_01xxxxx';
```

Bu değerleri kendi bilgilerinizle değiştirin:

```javascript
const PADDLE_VENDOR_ID = '12345'; // Paddle Dashboard'dan aldığınız Vendor ID
const PADDLE_PRICE_ID = 'pri_01xxxxx'; // Paddle Dashboard'dan aldığınız Price ID
```

## Adım 6: Production Moduna Geçiş

Test tamamlandıktan sonra production'a geçmek için:

1. `index.html` dosyasında şu satırı bulun:
```javascript
environment: 'sandbox' // Change to 'production' when ready
```

2. Şu şekilde değiştirin:
```javascript
environment: 'production'
```

## Adım 7: Webhook Kurulumu (Opsiyonel - Önerilir)

Ödeme bildirimlerini almak için webhook kurulumu yapmanız önerilir:

1. Paddle Dashboard'da **Developer Tools** > **Notifications** bölümüne gidin
2. **"Add Notification"** butonuna tıklayın
3. **Notification URL** girin (örnek: `https://yourdomain.com/webhook/paddle`)
4. Seçilecek event'ler:
   - `subscription.created`
   - `subscription.updated`
   - `subscription.cancelled`
   - `transaction.completed`
   - `transaction.payment_succeeded`
   - `transaction.payment_failed`

## Önemli Notlar

⚠️ **Güvenlik**:
- Vendor ID ve Price ID'yi frontend'de tutmak güvenlidir (Paddle bunu önerir)
- Webhook signature doğrulaması yapın (backend gereklidir)
- Hassas işlemler için backend entegrasyonu düşünün

✅ **Test Modu**:
- Sandbox modunda ödeme yaparken gerçek para çekilmez
- Test kartları kullanılabilir
- Production'a geçmeden önce test edin

📚 **Daha Fazla Bilgi**:
- Paddle Dokümantasyonu: https://developer.paddle.com/
- Paddle Checkout API: https://developer.paddle.com/api-reference/ZG9jOjM2MzE2MDM4-checkout

## Sorun Giderme

**Problem**: Paddle Checkout açılmıyor
- Çözüm: Vendor ID ve Price ID'nin doğru olduğundan emin olun
- Browser console'u kontrol edin (F12)

**Problem**: "Paddle is not loaded" hatası
- Çözüm: İnternet bağlantınızı kontrol edin, Paddle script'inin yüklendiğinden emin olun

**Problem**: Ödeme tamamlanmıyor
- Çözüm: Sandbox modunda test kartı bilgilerini kullanın
- Paddle Dashboard'da transaction loglarını kontrol edin

