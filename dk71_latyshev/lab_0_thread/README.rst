=================================================
**Лабораторна робота №0 Робота з потоками**
=================================================

 **Завдання:**
=================================================
  Для виконання завдання потрібно :
  - Завести глобальну змінну, яка ініціалізується в 0;

  - Створити фунцію потоку, яка буде прибавлять по K до значення N;

  - Запустити два потока з цією фунцією;

  - Дочекатися завершення, використовуючи метод `pthread_join()`;

  - Вивести в `stdout` очікуване та фактичне значення;

  - Створити `Makefile` використувуючи різну оптимізацію;

  - Додати до глобальної змінної `volatile `, зафіксувати зміни;

Хід роботи
------------------
**Написання програми**
Стандартно при початку роботи ми додали бібліотеки, для роботи з потоками підключити `<pthread.h>`.

Ми перевірили чи правильну кількість аругемнів було прийнято.

Таком ми маємо виконати Преобразование строки в значение типа `long`. Це виконано  через strtoul.

Створюэмо два потоки, створюємо їх через `pthread_create(&indiff_1, NULL, increment, &arg_val)`, де 
є ідентифікатор потоку,  функція що буде виконуватись в потоці та аргументне значення.
Та очікуємо кінець через `pthread_join()`
`
За для зручності перевірки результату роботи програми було написано MakeFile
Не потрібно витрачати зайвий час на пропис довгих команд, а досить написати 
невеликий  MakeFile.


Висновки
---------
В цій роботі я навчився працювати з MakeFile , зокрема з clang-format , це з лекції. Розібрався як руками проводити сборку в обьєктний файл та потім лінкувати.
Розібрався з флагами, як збирати, з форматом (в чому різниця між gnu18 та c18),також час був приділенний і рівням оптимізації, в нашому випадку це  ``O0`` та ``O2`` .
 При оплимізації ``O0`` результат не вірний по причині  порушення послідовності зчитування модифікування запису одного потоку іншим.
При оптимізації ``O2`` використовується лише в кінці під час виведення результату, і одказу записує до змінної результат інкрементації.
``volatile`` —  Модифікатор говорить про те, що ми будемо використовувати цю змінну різними потоками і вимагає від компілятора не розміщувати її для зберігання там, де ми не зможемо отримати до неї доступ.
 По суті в нас виникає "гонка даних", що нам і не дає отримати правильний результат.
``volatile``  ключове слово вказує на те, що значення може змінюватися між різними зверненнями, навіть якщо воно, здається, не модифікується. Це ключове слово 
заважає оптимізуючому компілятору оптимізувати подальші читання або записи і, таким чином, неправильно повторно використовує застаріле значення або пропускає записи.
Частково запозичений матеріал у Єсича, було занадто гарно щоб не взяти.                     