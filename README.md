# Web Party Games

Tarayıcıda arkadaşlarla oynanan, gerçek zamanlı çok oyunculu parti oyunları. Tek bir **FastAPI + WebSocket** sunucusu bütün oyunları yönetir. Oyuncular oda kodu ile aynı odaya katılır, oyun durumu sunucuda tutulur ve her değişiklik odadaki herkese anlık olarak gönderilir.

Bilgisayar ağları dersi için 4 kişilik bir ekip olarak geliştirildi.

## Oyunlar

| Oyun | Açıklama | WebSocket |
|---|---|---|
| **Pictionary** | Biri çizer, diğerleri tahmin eder. Tur sistemi, kelime maskeleme, puanlama | `/ws/pictionary` |
| **Spyfall** | Herkes konumu bilir, casus hariç. Sıra ile soru, oylama ve casusun tahmin hakkı | `/ws/spyfall` |
| **Codenames** | İki takım, ipucu veren kaptanlar, 5×5 kelime tablosu | `/ws/codenames` |
| **Tic-Tac-Toe** | Çok turlu XOX | `/ws/ttt` |
| **Pixel War** | Ortak tuvalde süreli alan kapma, tur sonunda skor hesabı | `/ws/pixelwar` |
| **Liar's Bar** | Blöf kart oyunu, "YALAN!" çağrısı ve rus ruleti cezası | `/ws/liars` |
| **Sumo Bash** | Daralan arenada çarpışma fiziğiyle itişme *(sadece sunucu tarafı)* | `/ws/sumobash` |

## Teknik detaylar
- **Backend:** Python, FastAPI, `asyncio`, WebSocket
- **Frontend:** Bağımlılıksız HTML, CSS ve JavaScript (`static/`)
- **Oda sistemi:** Oda kodu, isteğe bağlı oda şifresi ve davet anahtarı, host yönetimi
- **Durum senkronizasyonu:** Sunucu tek doğruluk kaynağıdır, her olaydan sonra odaya durum yayını (broadcast) yapılır
- **Zamanlayıcılar:** Tur süreleri, oylama ve arena daralması `asyncio` görevleriyle
- **Fizik (Sumo Bash):** Daire-daire çarpışma çözümü, itme ve arenadan düşme kontrolü
- Yardımcı uç noktalar: `GET /health`, `GET /rooms`
- Proje AWS EC2 üzerinde Nginx ve SSL ile yayınlandı

## Çalıştırma

```bash
python -m venv venv
venv\Scripts\activate          # macOS/Linux: source venv/bin/activate
pip install -r requirements.txt
uvicorn server:app --host 0.0.0.0 --port 8000
```

Tarayıcıda `http://localhost:8000` adresini aç. Aynı ağdaki arkadaşların da bilgisayarının IP adresiyle bağlanabilir.

## Ekip
- [@siyde](https://github.com/siyde)
- [@keremkafes](https://github.com/keremkafes)
- [@EfeAslangul](https://github.com/EfeAslangul)
- [@larakrdnz03](https://github.com/larakrdnz03)
