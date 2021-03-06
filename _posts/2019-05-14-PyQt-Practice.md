---
layout: page
title: PyQt Practice
tags: pyqt
key: page-single
---

Recently, I practice about PyQt library for GUI Program.  
I study PyQt while I follow up this book that link is <https://wikidocs.net/book/2165>  
You can read it for free!  
I practiced examples of the most of this book.  
  
And I programmed own my application using PyQt.  
That is 'Lotto Number Generator'.  

Sometimes, I see lotto number prediction of someone who is social influencer. (INSTAGRAM ID : @kkotppa_flower)  
The number of predicted number from him is more than 6 numbers.  
Then, I need to picked only 6 numbers. It is very complicated job to me.  
So I make the app for easier picking.  


```bash
import sys, random
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
from PyQt5.QtCore import *


class LottoApp(QWidget):
    def __init__(self):
        super().__init__()

        self.initUI()

    def initUI(self):

        
        self.first_input_lbl = QLabel('Enter the numbers 1 to 45')
        self.subexplain_lbl = QLabel('at least 6 numbers, ex) 1,2,3,4,5,6')
        subFont = self.subexplain_lbl.font()
        subFont.setPointSize(9)
        subFont.setBold(True)
        self.subexplain_lbl.setFont(subFont)
        self.used_num_le = QLineEdit()
        self.used_num_le.setPlaceholderText('Enter')
        self.used_num_le.setFocus()

        self.second_input_lbl = QLabel('Enter the times')
        self.ntimes_le = QLineEdit()
        self.ntimes_le.setPlaceholderText('If you want 1 time, enter only 1')
        self.ntimes_le.setValidator(QIntValidator(0, 99))

        self.generate_btn = QPushButton('Generation!')
        self.generate_btn.clicked.connect(self.validate)  # listener

        vBox = QVBoxLayout()
        vBox.addStretch(1)
        vBox.addWidget(self.first_input_lbl)
        vBox.addWidget(self.subexplain_lbl)
        vBox.addWidget(self.used_num_le)
        vBox.addStretch(1)
        vBox.addWidget(self.second_input_lbl)
        vBox.addWidget(self.ntimes_le)
        vBox.addStretch(1)
        vBox.addWidget(self.generate_btn)

        self.dialog = QDialog()

        self.setLayout(vBox)
        self.setWindowTitle('LottoApp')
        self.setGeometry(300, 100, 300, 200)
        self.show()

    def generate_lotto_num(self, num_list, times):
        num_list = list(map(int, num_list))
        result_str = ""
        for i in range(int(times)):
            temp_list = random.sample(num_list, 6)
            temp_list.sort()
            result_str += str(i+1) + "time -> " + str(temp_list) + "\n"

        self.result_lbl = QLabel()
        self.result_lbl.setText(result_str)

        resultBox = QVBoxLayout()
        resultBox.addWidget(self.result_lbl)
        self.dialog = QDialog()
        self.dialog.setLayout(resultBox)
        self.dialog.setWindowTitle('LottoApp - Result')
        self.dialog.setGeometry(300, 300, 300, 300)
        self.dialog.show()


    def validate(self):
        if self.used_num_le.text() == '' or self.ntimes_le.text() == '' :
            QMessageBox.warning(self, 'WARN', 'Please Fill the blank', QMessageBox.Yes)
        else:
            used_num_list = list(set(self.used_num_le.text().split(",")))
            ntime = self.ntimes_le.text()
            print("num list : " + str(used_num_list))
            if len(used_num_list) < 6:
                QMessageBox.warning(self, 'WARN', 'Please Enter the numbers at least 6 numbers. No Redundant', QMessageBox.Yes)
            else:
                self.generate_lotto_num(used_num_list, ntime)


if __name__ == '__main__':

    app = QApplication(sys.argv)
    ex = LottoApp()
    sys.exit(app.exec_())
```
