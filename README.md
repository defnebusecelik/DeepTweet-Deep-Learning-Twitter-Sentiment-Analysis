# Twitter Sentiment Classification

Bu proje, Twitter’dan elde edilen geniş ölçekli “Sentiment140” veri setini kullanarak her bir tweet’i **pozitif** veya **negatif** olarak sınıflandıran bir makine öğrenmesi altyapısı sunar. Hız ve kaynak verimliliği ön planda tutularak çeşitli derin öğrenme mimarileri karşılaştırılmıştır.


## 1. Veri Seti

* **Kaynak**: Kaggle “Sentiment140 dataset with 1.6 million tweets” \[8]
* **Toplam Örnek**: 1.600.000 tweet (800.000 pozitif, 800.000 negatif)
* **Kullanılan Sütunlar**: `Sentiment` (0 = negatif, 4 = pozitif), `Tweet`


## 2. Önişleme Adımları

1. **Sütun Eleme**: `Id`, `Date`, `Flag`, `User` atıldı.
2. **Temizlik**: `@mention`, URL, özel karakterler kaldırıldı.
3. **Tokenizasyon**: Boşluk bazlı ve `BertTokenizerFast` ile subword tokenizasyonu.
4. **Durak Kelime Temizliği**: NLTK stop-word, “not” çıkarılmadı.
5. **Lemmatizasyon & Stemming**: `WordNetLemmatizer`, `PorterStemmer`.
6. **Padding & Masking**: `max_len` = 24/32 token.
7. **Stratified Alt Örnekleme**: Eğitim verisinin %8–25’i.


## 3. Test Edilen Modeller

* **CNN + BiLSTM**
* **CNN + LSTM**
* **MLP**
* **Tek Katmanlı LSTM**
* **Gürültü Destekli LSTM**
* **Transformer & BERT Tabanlı**


## 4. Performans Sonuçları

|       Model       | Veri % | Test Accuracy | Test Loss |
| :---------------: | -----: | ------------: | --------: |
|    CNN + BiLSTM   |   20 % |       78.54 % |    0.5218 |
|    CNN + BiLSTM   |   15 % |       78.23 % |    0.5519 |
|     CNN + LSTM    |   10 % |       77.34 % |    0.5277 |
|        MLP        |   10 % |       75.55 % |    0.5454 |
| Tek Katmanlı LSTM |   25 % |       78.76 % |    0.4482 |
| Tek Katmanlı LSTM |   12 % |       74.62 % |    0.4193 |
|   Gürültülü LSTM  |   12 % |       69.99 % |    0.6488 |