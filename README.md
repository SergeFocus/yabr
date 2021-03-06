# Yet another brace reader: Чтение "скобкофайлов" 1С (yabr)
Библиотека чтения скобочных файлов 1С.

Читает скобочный файл в иерархию структур и массивов:

    |-> Элемент
    |      |- Родитель    - родительский элемент (Неопределено - для корневого элемента)
    |______|________|
    |      |- Уровень     - уровень элемента в иерархии (0 - корневой элемент)
    |      |- Индекс      - индекс элемента в родительском элементе
    |      |- НомераСтрок - соответствие с номерами строк исходного файла, на основании которых создан текущий и подчиненные элементы
    |      |- Значения    - массив дочерних элементов
    |_______________|

Кратко:
 - пока в виде обработки 1С (в билиотеку позднее будет завернуто)
 - Основная функция "ПрочитатьСкобкофайл"
 - Чтение выполняется последовательно по строкам
 - Ошибки формата файла не проверяются и игнорируются, что сможет прочитать. то и получится
 - Все читается в структуру указанную выше
 - Для закрывающихся скобок ("}") реализован вызов процедуры-обработчика в привязке к уровню вложенности скобок
    - обработчики привязываются к уровню элемента в иерархии
    - добавление обработчиков прописывается в процедуре "ПолучитьПравилаОбработки"
 - Обработанные элементы могут быть удалены из прочитанного массива после обработке
 - В обработке реализованы примеры обработчиков для:
    - формата описания параметров кластера
    - текстового формата журнала регистрации
    - формата "словаря" журнала регистрации
- Журнал регистрации в настоящий момент читается со скоростью ~1300 строк/сек

В планах:
 - реализовать пропуск ранее прочитанныч строк (для экспорта журнала регистрации, т.к. он большой)
 - Реализовать os-библиотеку на основе обработки
 - оптимизация скорости чтения файлов