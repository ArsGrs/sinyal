sinyal-dashboard/
│
├── dashboard/
│   ├── pages/
│   │   └── index.tsx           ← Halaman utama: grafik + sinyal
│   ├── components/
│   │   └── CryptoChart.tsx     ← Komponen grafik harga
│
├── bot/
│   └── bot.py                  ← Script bot Telegram kirim sinyal ETH/BTC
│
├── utils/
│   └── signal_logic.py         ← Logika sinyal beli/jual berdasarkan harga
│
├── requirements.txt            ← Dependensi Python untuk bot
├── README.md
└── vercel.json                 ← Untuk auto deploy ke web# sinyal
