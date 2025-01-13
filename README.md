UAS 1 , SOAL 1
#include <iostream>

using namespace std;

double mencarideterminan(int data[3][3]) {
	int determinan = (data[0][0] * data[1][1] * data[2][2] 
					+ data[0][1] * data[1][2] * data[2][0]
					+ data[0][2] * data[1][0] * data[2][1])
					- (data[2][0] * data[1][1] *data[0][2] 
					+ data[2][1] * data[1][2] * data[0][0] 
					+ data[2][2] * data[1][0] * data[0][1]);
	return determinan;
}

void mencariKofaktor(int data[3][3], int kofaktor[3][3]) {
    kofaktor[0][0] = data[1][1] * data[2][2] - data[1][2] * data[2][1];
    kofaktor[0][1] = -(data[1][0] * data[2][2] - data[1][2] * data[2][0]);
    kofaktor[0][2] = data[1][0] * data[2][1] - data[1][1] * data[2][0];

    kofaktor[1][0] = -(data[0][1] * data[2][2] - data[0][2] * data[2][1]);
    kofaktor[1][1] = data[0][0] * data[2][2] - data[0][2] * data[2][0];
    kofaktor[1][2] = -(data[0][0] * data[2][1] - data[0][1] * data[2][0]);

    kofaktor[2][0] = data[0][1] * data[1][2] - data[0][2] * data[1][1];
    kofaktor[2][1] = -(data[0][0] * data[1][2] - data[0][2] * data[1][0]);
    kofaktor[2][2] = data[0][0] * data[1][1] - data[0][1] * data[1][0];
}
bool mencariInvers(int data[3][3], double invers[3][3]) {
    double determinan = mencarideterminan(data);
     if (determinan == 0) {
        cout << "Matriks tidak memiliki invers karena determinan = 0" << endl;
        return false;
     }
     else {
        int kofaktor[3][3];
        mencariKofaktor(data, kofaktor);
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                invers[i][j] = (double)kofaktor[j][i] / determinan;
            }
        }
        return true;
     }
}


int main() {
    int matriks[3][3] =
    { 4,2,8,
     2,1,5,
     3,2,4 };
   

    cout << "matrik awal = " << endl;
    for (int i = 0; i < 3; i++) {
        for (int  j= 0; j < 3; j++){
            cout << matriks[i][j] << ", ";
        }
        cout << endl;
    }

    //MENCARI INVERS
    double invers[3][3];
    cout << mencariInvers(matriks,invers);

    cout << "nilai invers matrik  = " << endl;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << invers[i][j] << ", ";
        }
        cout << endl;
    }




	return 0; 
}




UAS 2 , SOAL 2
#include <iostream>
#include <algorithm>
#include <cmath>
using namespace std;

double mencarimean(int data[], int panjangdata) {
    int jumlahdata = 0;
    for (int i = 0; i < panjangdata; i++) {
        jumlahdata += data[i];
    }
    double mean = (double)jumlahdata / panjangdata;
    return mean;
}

double mencariMedian(int data[], int panjangdata) {
    sort(data, data + panjangdata);
    if (panjangdata % 2 == 0) {
      int mediangenap = (data[panjangdata / 2 - 1] + data[panjangdata / 2]) / 2.0;
      return mediangenap;
    }
    else {
       int medianganjil= data[panjangdata+1 / 2];
       return medianganjil;
    }
}

double mencariStandardDeviation(int data[], int panjangdata, double mean) {
    double total = 0;
    for (int i = 0; i < panjangdata; i++) {
        total += pow(data[i] - mean, 2);
    }
    double StandardDeviasi = sqrt(total / panjangdata);
    return StandardDeviasi;
}

int main() {

    int data[] = { 92, 65, 74, 80, 80, 70, 78 };
    int panjangdata = sizeof(data) / sizeof(data[0]);

    // Mencari mean
    double mean = mencarimean(data, panjangdata);
    cout << "Nilai mean adalah = " << mean << endl;
    // mencari median
    double median = mencariMedian(data, panjangdata);
    cout << "Nilai median adalah = " << median << endl;
    //mencari standart deviasi
    double standardeviasi = mencariStandardDeviation(data, panjangdata, mean);
    cout << "Nilai standartdeviasi adalah = " << standardeviasi << endl;

    sort(data, data + panjangdata);
    cout << data[1];


    return 0;
}
