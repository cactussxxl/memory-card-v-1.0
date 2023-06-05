# memory-card-v-1.0
from PyQt5.QtCore import Qt
from PyQt5.QtWidgets import (QApplication, QWidget, QHBoxLayout, QVBoxLayout, QGroupBox, QButtonGroup, QRadioButton, QPushButton, QLabel)
from random import shuffle
from random import randint



class Question():
    def __init__(self, question, right_answer, wrong1, wrong2, wrong3):
        #все строки надо задать при создании объекта, они запоминаются в свойствах
        self.question = question
        self.right_answer = right_answer
        self.wrong1 = wrong1
        self.wrong2 = wrong2
        self.wrong3 = wrong3


question_list = []
question_list.append(Question('Государственный язык Бразилии', 'Португальский', 'Английский', 'Испанский', 'Бразильский'))
question_list.append(Question('Какого цвета нет на флаге России', 'Зелёный', 'Красный', 'Белый', 'Синий'))
question_list.append(Question('Национальная хижина якутов', 'Ураса', 'Юрта', 'Иглу', 'Хата'))
question_list.append(Question('Год создания YouTube', '2005', '2009', '2003', '2004'))
question_list.append(Question('Кто такой Никита?', 'Никита', 'Самурай', 'Программист', 'Умный человек'))
question_list.append(Question('Цвет, котрого нет на радуге', 'Розовый', 'Зелёный', 'Голубой', 'Фиолетовый'))
question_list.append(Question('Как называется приспособление для игры на гитаре?', 'Плектр', 'Резистор', 'Медиа плеер', 'Шаффл'))
question_list.append(Question('Если жёлтый мячик бросить в чёное море, то каким он будет?', 'Мокрым', 'Чёрным', 'Жёлтым', 'Солёным'))
question_list.append(Question('Суббренд Xiaomi', 'Wiha', 'Galaxy', 'Oppo', 'Phone'))
question_list.append(Question('Нотбук от ASUS', 'VivoBook', 'ThinkPad', 'Aspire', 'Omen'))
question_list.append(Question('Самое популярное слово в мире', 'Ок', 'Привет', 'Хорошо', 'Я'))
question_list.append(Question('Самое длинное слово на русском языке ', 'Тетрагидропиранилциклопентилтетрагидропиридопиридиновые', 'Метоксихлордиэтиламинометилбутиламиноакридингемоглин', 'Хлебосколбаскойлюбезнопроизводительный', 'Говядина'))
question_list.append(Question('Самый красивый язык', 'Итальянский', 'Арабский', 'Китайский', 'Украинский'))
question_list.append(Question('Самая большая планета в солнечной системе', 'Юпитер', 'Сатурн', 'Земля', 'Плутон'))
question_list.append(Question('Год становления Казахстана независимым', '1991', '1945', '1465', '1990'))




    
app = QApplication([])
btn_OK = QPushButton('Ответить') 
lb_Question = QLabel('Самый сложный вопрос в мире!')
 
RadioGroupBox = QGroupBox("Варианты ответов") 
rbtn_1 = QRadioButton('Вариант 1')
rbtn_2 = QRadioButton('Вариант 2')
rbtn_3 = QRadioButton('Вариант 3')
rbtn_4 = QRadioButton('Вариант 4')
 
RadioGroup = QButtonGroup()
RadioGroup.addButton(rbtn_1)
RadioGroup.addButton(rbtn_2)
RadioGroup.addButton(rbtn_3)
RadioGroup.addButton(rbtn_4)
layout_ans1 = QHBoxLayout()   
layout_ans2 = QVBoxLayout() 
layout_ans3 = QVBoxLayout()
layout_ans2.addWidget(rbtn_1)
layout_ans2.addWidget(rbtn_2)
layout_ans3.addWidget(rbtn_3) 
layout_ans3.addWidget(rbtn_4)
 
layout_ans1.addLayout(layout_ans2)
layout_ans1.addLayout(layout_ans3) 
 
RadioGroupBox.setLayout(layout_ans1) 
 
AnsGroupBox = QGroupBox("Результат теста")
lb_Result = QLabel('прав ты или нет?')
lb_Correct = QLabel('ответ будет тут!')
 
layout_res = QVBoxLayout()
layout_res.addWidget(lb_Result, alignment=(Qt.AlignLeft | Qt.AlignTop))
layout_res.addWidget(lb_Correct, alignment=Qt.AlignHCenter, stretch=2)
AnsGroupBox.setLayout(layout_res)
 
layout_line1 = QHBoxLayout()
layout_line2 = QHBoxLayout()
layout_line3 = QHBoxLayout()
 
layout_line1.addWidget(lb_Question, alignment=(Qt.AlignHCenter | Qt.AlignVCenter))
layout_line2.addWidget(RadioGroupBox)   
layout_line2.addWidget(AnsGroupBox)  
AnsGroupBox.hide() 
 
layout_line3.addStretch(1)
layout_line3.addWidget(btn_OK, stretch=2) 
layout_line3.addStretch(1)
 
layout_card = QVBoxLayout()
 
layout_card.addLayout(layout_line1, stretch=2)
layout_card.addLayout(layout_line2, stretch=8)
layout_card.addStretch(1)
layout_card.addLayout(layout_line3, stretch=1)
layout_card.addStretch(1)
layout_card.setSpacing(5)
 
def show_result():
    ''' показать панель ответов '''
    RadioGroupBox.hide()
    AnsGroupBox.show()
    btn_OK.setText('Следующий вопрос')
 
def show_question():
    ''' показать панель вопросов '''
    RadioGroupBox.show()
    AnsGroupBox.hide()
    btn_OK.setText('Ответить')
    RadioGroup.setExclusive(False) 
    rbtn_1.setChecked(False)
    rbtn_2.setChecked(False)
    rbtn_3.setChecked(False)
    rbtn_4.setChecked(False)
    RadioGroup.setExclusive(True) 
 
answers = [rbtn_1, rbtn_2, rbtn_3, rbtn_4]
 
def ask(q: Question):
    ''' функция записывает значения вопроса и ответов в соответствующие виджеты, 
    при этом варианты ответов распределяются случайным образом'''
    shuffle(answers)
    answers[0].setText(q.right_answer)
    answers[1].setText(q.wrong1)
    answers[2].setText(q.wrong2)
    answers[3].setText(q.wrong3)
    lb_Question.setText(q.question)
    lb_Correct.setText(q.right_answer) 
    show_question() 
 
def show_correct(res):
    ''' показать результат - установим переданный текст в надпись "результат" и покажем нужную панель '''
    lb_Result.setText(res)
    show_result()
 
def check_answer():
    ''' если выбран какой-то вариант ответа, то надо проверить и показать панель ответов'''
    if answers[0].isChecked():
        show_correct('Правильно!')
        window.score += 1
        print('Сатистика\n-Всего вопросов: ', window.total, '\n-Правильных ответов: ',window.score )
    else:
        if answers[1].isChecked() or answers[2].isChecked() or answers[3].isChecked():
            show_correct('Неверно!')
            print('Рейтинг:', (window.score/window.total*100),)


def next_question():
    '''задает  следущий вопрос из списка'''
    window.total += 1
    print('Статистика\n-Всего вопросов:', window.total, 'n\-Правильных ответов:', window.score)
    cur_question = randint(0, len(question_list)-1 )
    
    #если список вопросов закончился - идём сначала
    q = question_list[cur_question]#взяли вопрос
    ask(q)#спросили


def click_OK():
    '''определяет, надо ли показывать другой вопрос либо проверитт ответ на этот'''
    if btn_OK.text() == 'Ответить':
        check_answer()
    else:
        next_question()

window = QWidget()
window.setLayout(layout_card)
window.setWindowTitle('Memo Card')
#теущий вопрос из списка сделаем свойством объекта 'окно', так мы сможем спокойно менять его из функции:


btn_OK.clicked.connect(click_OK) 

window.score = 0
window.total = 0
next_question()
window.resize(400,300)
window.show()
app.exec()
