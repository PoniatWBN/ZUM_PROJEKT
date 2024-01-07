PRZEGLĄD

Zawiera 34 686 770 recenzji Amazon od 6 643 669 użytkowników na temat 2 441 053 produktów, z projektu Stanford Network Analysis Project (SNAP). Podzbiór ten zawiera 1 800 000 próbek szkoleniowych i 200 000 próbek testowych dla każdego sentymentu polaryzacji.

POCHODZENIE

Zbiór danych recenzji Amazon składa się z recenzji z Amazon. Dane obejmują okres 18 lat i obejmują około 35 milionów recenzji do marca 2013 r. Recenzje obejmują informacje o produktach i użytkownikach, oceny oraz recenzje w postaci zwykłego tekstu. Więcej informacji można znaleźć w artykułach: J. McAuley i J. Leskovec. Ukryte czynniki i ukryte tematy: zrozumienie wymiarów ocen na podstawie tekstu recenzji. RecSys, 2013.

OPIS

Zbiór danych zawiera dane o polaryzacji recenzji Amazona. W zbiorze danych klasa 1 jest ujemna, a klasa 2 jest pozytywna. Każda klasa ma 1 800 000 próbek szkoleniowych i 200 000 próbek testowych.

UWAGI

Z uwagi na duży rozmiar zbioru użytego podczas wykonywanego eksperymentu, dochodziło do liczbych przeciążeń ramowych. Dlatego też w jednym z pierwszych kroków postanowiłem zmniejszyć zbiór, by dane eksperyment wykonać. W przypadku posiadania większej zdolności obliczeniowej można podejść do eksperymentu ponownie już na pełnym zbiorze. Z uwagi na podzial zbioru, postanowiłem ponownie zbadać rozłożenie poszczególnych klas, ich liczba jest zbliżona, dlatego też postanowiłem kontynuować eksperyment.


LINK:
https://www.kaggle.com/code/purvitsharma/amazon-reviews-bidirectional-lstm?fbclid=IwAR2T8qe_2KR9IAM-vSJDDBH9EwThlC7on3b4CRHcnDO_AMBDtguZXtgP1cM


OPIS MODELU LSTM:

Parametry wejściowe:
- embedding Dimension - 64 (oznacza to, że każe ze słów w sekwencji wejściowej bedzie reprezentowane jako 64-wymiarowy wektor)
- Vocabulary size - 1 000 000 - model bedzie rozpoznawać maksymalnie milion unikalnych słów
- Max Lenght - Długść każdej przetwrazanej sekwencji bedzie ograniczona do 64 tokenów

Budowa sieci LSTM składa się z następujących warstw
1 - Warstwa Enbeddingowa:
Zadaniem warstwy jest przetworzenie słowa w sekwencji wejścia na embedding o wymiarach 64, a także z pozostałymi funkcjami parametrów takimi jak maksymalna długosc sekwencji i liczba słó w input, a także zdefiniowanie outputu warstwy/.
2 - Warstwa LSTM
Warstwa skłąda się z 32 jednostek będąćych komórkami pamięci. Dodatkowo ustawiam zwracanie sekwencji wyjściowej dla każdego kroku czasowego.
3 - Warstwa Dropout
Warstwa regularyzacyjna, w której 0,2 (20%) jednostek będzie ignorowane podczas treningu. Funkcją warstwy bedzie unikniecie nadmiernego dopasowania.
4 - Druga warstwa LSTM
Warstwa o zblizonej budowanie do warstwy 2, jednak nie zwraca wymiarowego wektora, a pojedynczy wektor.
5 - Warstwa Dense
Warstwa gęsta z jednym neuronem, aktywowana funkcją sigmoid. Warstwa umożliwia binarne określenie sentymentu pomiedzy pozytywnym, a negatywnym.


Przy kompilacji modelu użyłem:
optymalizator adam, funkcja straty binary_crossentropy (jeden z typowych wyboroów przy klasyfikacji binarnej). Wyniki uczenia badane beda przyt użyciu accuracvy.


