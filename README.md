# Simple E-Commerce API

Öğrenciler için hazırlanmış, Docker ile tek komutla çalıştırılabilen e-ticaret REST API'si.

## Hızlı Başlangıç

### Gereksinimler
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

### Kurulum

```bash
# 1. Bu repoyu klonlayın
git clone https://github.com/matanist/SimpleECommerceDocker.git
cd SimpleECommerceDocker

# 2. Docker Compose ile başlatın
docker compose up -d

# 3. Tarayıcıda açın
# http://localhost:5000/swagger
```

İlk başlatmada build işlemi birkaç dakika sürebilir. Sonraki başlatmalar çok daha hızlı olacaktır.

> ✅ **Platform Uyumluluğu:** Bu proje hem **Windows/Linux (x86_64)** hem de **macOS Apple Silicon (M1/M2/M3)** üzerinde çalışır.

---

## Varsayılan Admin Kullanıcı

| Email | Şifre | Rol |
|-------|-------|-----|
| `admin@simpleecommerce.com` | `Admin123!` | Admin |

> Yeni kullanıcılar `/api/auth/register` ile kayıt olduğunda otomatik olarak "Customer" rolü atanır.

---

## API Endpoints

### Auth (Kimlik Doğrulama)
| Method | Endpoint | Açıklama |
|--------|----------|----------|
| POST | `/api/auth/login` | Giriş yap |
| POST | `/api/auth/register` | Kayıt ol |
| GET | `/api/auth/me` | Mevcut kullanıcı bilgisi |

### Categories (Kategoriler)
| Method | Endpoint | Açıklama |
|--------|----------|----------|
| GET | `/api/categories` | Tüm kategoriler |
| GET | `/api/categories/{id}` | Kategori detayı |
| POST | `/api/categories` | Yeni kategori (Admin) |
| PUT | `/api/categories/{id}` | Güncelle (Admin) |
| DELETE | `/api/categories/{id}` | Sil (Admin) |

### Products (Ürünler)
| Method | Endpoint | Açıklama |
|--------|----------|----------|
| GET | `/api/products` | Tüm ürünler (sayfalama destekli) |
| GET | `/api/products/{id}` | Ürün detayı |
| POST | `/api/products` | Yeni ürün (Admin) |
| PUT | `/api/products/{id}` | Güncelle (Admin) |
| DELETE | `/api/products/{id}` | Sil (Admin) |

### Orders (Siparişler)
| Method | Endpoint | Açıklama |
|--------|----------|----------|
| GET | `/api/orders` | Tüm siparişler (Admin) |
| GET | `/api/orders/my-orders` | Kendi siparişlerim |
| POST | `/api/orders` | Yeni sipariş |
| PUT | `/api/orders/{id}/status` | Durum güncelle (Admin) |
| POST | `/api/orders/{id}/cancel` | İptal et |

### Users (Kullanıcılar)
| Method | Endpoint | Açıklama |
|--------|----------|----------|
| GET | `/api/users` | Tüm kullanıcılar (Admin) |
| GET | `/api/users/{id}` | Kullanıcı detayı |
| PUT | `/api/users/{id}` | Güncelle |
| DELETE | `/api/users/{id}` | Sil (Admin) |

---

## Örnek Kullanım

### 1. Giriş Yapma

```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@simpleecommerce.com","password":"Admin123!"}'
```

### 2. Ürünleri Listeleme

```bash
curl http://localhost:5000/api/products
```

### 3. Sipariş Oluşturma (Token gerekli)

```bash
curl -X POST http://localhost:5000/api/orders \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{"items":[{"productId":1,"quantity":2}]}'
```

---

## Hazır Veriler

API başlatıldığında otomatik olarak **300 ürün** ve **10 kategori** oluşturulur:

### Kategoriler
- Electronics, Clothing, Books, Home & Garden, Sports & Outdoors
- Toys & Games, Health & Beauty, Automotive, Food & Beverages, Office Supplies

---

## Durdurma ve Silme

```bash
# Durdur
docker compose down

# Durdur ve verileri sil
docker compose down -v
```

> ⚠️ **Önemli Not:** Eğer `docker compose up` çalıştırırken veritabanı container'ı "unhealthy" hatası veriyorsa, eski volume'u silmeniz gerekir:
> ```bash
> docker compose down -v
> docker compose up -d
> ```
> Docker Desktop kullanıyorsanız, container'ları silmenin yanı sıra **Volumes** sekmesinden `sqlserver-data` volume'unu da silmeyi unutmayın.

---

## Kaynak Kod

Projenin detaylı kaynak koduna erişmek için: [SimpleECommerceForTraining](https://github.com/matanist/SimpleECommerceForTraining)

## Teknolojiler

- .NET 9 Web API
- Entity Framework Core
- Azure SQL Edge (ARM64 + x86_64 uyumlu)
- JWT Authentication
- Swagger/OpenAPI
- Docker

---

## Lisans

MIT License
