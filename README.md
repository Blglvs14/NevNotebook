# NevNotebook
https://www.kaggle.com/code/bmzeynepner/nevnotebook

<b>Dipnot</b>t: İlk defa ReadMe yazıyorum. Geliştirmeye de vaktim olmadı, çirkinliğinin ve karışıklığının kusuruna bakmayın :)

df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 30000 entries, 0 to 29999
Data columns (total 18 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   url                 30000 non-null  object 
 1   source              30000 non-null  object 
 2   label               30000 non-null  object 
 3   url_length          30000 non-null  int64  
 4   starts_with_ip      30000 non-null  bool   
 5   url_entropy         30000 non-null  float64
 6   has_punycode        30000 non-null  bool   
 7   digit_letter_ratio  30000 non-null  float64
 8   dot_count           30000 non-null  int64  
 9   at_count            30000 non-null  int64  
 10  dash_count          30000 non-null  int64  
 11  tld_count           30000 non-null  int64  
 12  domain_has_digits   30000 non-null  bool   
 13  subdomain_count     30000 non-null  int64  
 14  nan_char_entropy    30000 non-null  float64
 15  has_internal_links  30000 non-null  bool   
 16  whois_data          23408 non-null  object 
 17  domain_age_days     20931 non-null  float64
dtypes: bool(4), float64(4), int64(6), object(4)
memory usage: 3.3+ MB


df.isnull().sum()
label
phishing      15145
legitimate    14855
Name: count, dtype: int64


df['label'].value_counts() 
url                      0
source                   0
label                    0
url_length               0
starts_with_ip           0
url_entropy              0
has_punycode             0
digit_letter_ratio       0
dot_count                0
at_count                 0
dash_count               0
tld_count                0
domain_has_digits        0
subdomain_count          0
nan_char_entropy         0
has_internal_links       0
whois_data            6592
domain_age_days       9069
dtype: int64


df = df.dropna(subset=['domain_age_days', 'whois_data'])


df['label'].value_counts()  
label
legitimate    13043
phishing       7888
Name: count, dtype: int64


plt.figure(figsize=(10, 6))
sns.countplot(x='label', data=df)
plt.title('Sınıf Dağılımı')
plt.xlabel('Sınıf')
plt.ylabel('Sayı')
plt.xticks(ticks=[0, 1], labels=['Phishing', 'Benign'])  # Etiketleri güncelle
plt.show()
![__results___9_0](https://github.com/user-attachments/assets/dcf2b3c6-910e-4e0e-aeb5-0831e32fdc2c)


plt.figure(figsize=(12, 6))
sns.barplot(x='source', y='label', data=df, estimator=lambda x: len(x) / len(df) * 100)  # Yüzde olarak gösterim
plt.title('Kaynaklara Göre Sınıf Dağılımı')
plt.xlabel('Kaynak')
plt.ylabel('Yüzde')
plt.xticks(rotation=45)
plt.show()
![__results___10_0](https://github.com/user-attachments/assets/16f33927-f14e-43bd-8ec6-d4b2fdcf36c1)


Denetimli Öğrenme Çıktıları:

Model: Logistic Regression
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   0 2363]]

 Model: SVM
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   2 2361]]

 Model: Decision Tree
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   0 2363]]

 Model: Random Forest
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   0 2363]]

Model: Gradient Boosting
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   0 2363]]

 Model: AdaBoost
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   0 2363]]

 Model: .Naive Bayes
              precision    recall  f1-score   support

           0       0.72      1.00      0.84      3917
           1       1.00      0.37      0.54      2363

    accuracy                           0.76      6280
   macro avg       0.86      0.68      0.69      6280
weighted avg       0.83      0.76      0.73      6280

[[3916    1]
 [1489  874]]

 Model: Neural Network
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   0 2363]]

 Model: K-Nearest Neighbors
              precision    recall  f1-score   support

           0       1.00      1.00      1.00      3917
           1       1.00      1.00      1.00      2363

    accuracy                           1.00      6280
   macro avg       1.00      1.00      1.00      6280
weighted avg       1.00      1.00      1.00      6280

[[3917    0]
 [   3 2360]]

 Best Model: Logistic Regression with Accuracy: 1.0



Denetimsiz Öğrenme Çıktıları:
Model: KMeans, Silhouette Score: 0.3313
Model: Agglomerative Clustering, Silhouette Score: 0.2785
Model: DBSCAN, Silhouette Score: 0.6192
Best Model: DBSCAN with Silhouette Score: 0.6192
