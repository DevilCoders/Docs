# Формы бронирвания

В проекте есть 3 формы бронирования: Авиа, ЖД, Отели (в будущем добавятся автобусы).

Все эти формы построены на едином стеке технологий и компонентов.

## BookingLayout

Набор компонетов которые управляют расположением основных блоков на странице бронирования.
На основе deviceType сами перекомпановывают расположение блоков.

<table>
    <tr>
        <td>
            <img src="./images/desktopLayout.png" height="600px" />
        </td>
        <td>
            <img src="./images/mobileLayout.png" height="600px" />
        </td>
        <td>
            <ol>
                <li>BookingLayout</li>
                <li>BookingLayout.Breadcrumbs</li>
                <li>BookingLayout.Forms</li>
                <li>BookingLayout.Snippets</li>
                <li>BookingLayout.Cart</li>
                <li>BookingLayout.CartCaption</li>
                <li>BookingLayout.Card - CardWithDeviceLayout</li>
            </ol>
        </td>
    </tr>
</table>

## BookingPassengerForm

<table>
    <tr>
        <td>С интентами</td>
        <td>Без интентов</td>
    </tr>
    <tr>
        <td>
            <img src="./images/withIntents.png" height="250px" />
        </td>
        <td>
            <img src="./images/withoutIntents.png" height="250px" />
        </td>
    </tr>
</table>

Компонент формы для заполнения данных пассажира. Имеет компановки с 3 наборами полей:

1. фамилия, имя (отели) - однострочная форма с 2мя полями;
2. фамилия, имя, пол, дата рождения, поля заполенения документа (зарубежные авиа перелеты) - форма с расположением полей в 2 строки;
3. фамилия, имя, отчество, пол, дата рождения, поля заполенения документа (ЖД, авиа перелеты по РФ) - форма с полями в 3 строки;

[Примеры использования](../../src/components/BookingPassengerForm/README.md);

## BookingContactsForm

<img src="./images/contacts.png" height="150px" />

Простой компонент формы для заполнения контактов.

[Примеры использования](../../src/components/BookingContactsForm/README.md);
