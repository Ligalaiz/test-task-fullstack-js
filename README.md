# Тестовое задание Fullstack JavaScript

Задание рассчитано на 3 часа выполнения (при условии, что соискатель знаком с необходимыми технологиями, и ресёрч сводится к минимуму).

Использование фреймворков, библиотек или npm-модулей, написанных не Вами, не предполагается.
Использовать модули из стандартной поставки NodeJS нужно.

## Проект Proof of Concept "Front and Back on JS"

### Backend

Сервер на NodeJS должен работать в качестве файлового сервера (выдавать файлы для работы Frontend-части) и принимать/отдавать данные по API (3 эндпоинта):

1. POST для добавления нового сообщения
2. POST для отправки следующего числа и получения среднего между ним и предыдущим в ответ
3. GET для получения информации обо всех предыдущих числах и расчётах

### Frontend

Три страницы:

1. О себе. Статический HTML с краткой информацией - несколько предложений, фотография.
2. Доска сообщений с рендером предыдущих на стороне сервера (SSR) и формой добавления нового сообщения.
3. Средние числа. Ввод числа в простую форму, отправка запроса на сервер, получение среднего числа в ответ, вывод результата над предыдущими. Рендер на стороне клиента (CSR).

## Детали реализации

На всех страницах стили - предельно простой легко читаемый минимализм. Без изысков. Адаптив не нужен, но информация должна помещаться на экране по умолчанию.

### страница Доска сообщений

- при входе на страницу сервер формирует и выдаёт HTML-разметку с включением данных уже полученных сообщений (на старте сервера - одно захардкоденное сообщение)
- каждое сообщение на экране состоит из значений полей `text` и `author`
- кроме сообщений на странице находится форма размещения нового сообщения c теми же полями и кнопкой "разместить сообщение"
- при отправке сообщения выполняется обновление страницы после которого новое сообщение должно появиться рядом с предыдующими (первым или последним - в зависимости от порядка сортировки)
- сервер может хранить сообщения в массиве в памяти или (необязательно) в файле.

### страница Средние числа

- пользователь вводит число в форму, сам отмечает, если число отрицательное и/или дробное (например галочками)
- при нажатии кнопки "отправить и получить среднее" выполняется отправка запроса к серверу на соответствующий API-эндпоинт
- запрос и обработка ответа на клиенте посредством JavaScript
- сервер в ответ присылает предыдущее число, последнее принятое от пользователя и среднее между ними
- клиент выводит их под формой новой строкой (из неё должно быть понятно, где что)
- данные предыдущих расчётов сдвигаются вниз
- при входе/обновлении страницы приходящая от сервера HTML-разметка не содержит данных о предыдующих расчётах
- клиент сразу отправляет запрос, после получения ответа на который под формой выводится история предыдущих полученных и вычисленных чисел

### Обязательно

- сервер не должен падать при запросах на получение отсутствующих файлов или на непредусмотренные API-эндпоинты
- сервер должен отдавать клиенту только публичные файлы (файлы бэкенда выдаваться не должны)
- должен быть API-эндпоинт, принимающий число из строки запроса

### Желательно

- страница 404, адекватно дающая понять, что запрошенного файла нет, стили на ней не принципиальны, но если они есть, то должны быть включены в разметку и не требовать отдельных запросов
- отличимый префикс API-эндпоинтов
- API-эндпоинт, принимающий число и возвращающий среднее, учитывает знак и/или дробную часть числа лишь если соответствующие флаги в форме были установлены, и отметки об этом были в пришедшем на сервер запросе
- API-эндпоинт