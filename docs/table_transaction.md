Таблица `transaction`
============

Содержит операции для транзакций.

Есть несколько типов операций, которые определяются в поле `operation`.

PAYOUTER_SYSTEM - это приход на кошелек денег из внешней системы.
таким образов в полях таблицы будут следующие значения:
`account_type = null`.

IN - это зачисление с платежной системы.
таким образов в полях таблицы будут следующие значения:
`account_type = null`.

REF_IN - прибыль от лично приглашенных.

# Поля

<table>
    <tr>
        <td>id</td>
        <td> INT(11)</td>
        <td> NOT NULL AUTO_INCREMENT,</td>
    </tr>
    <tr>
        <td>date</td>
        <td> DATETIME</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>sum</td>
        <td> DECIMAL(19, 4)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>account</td>
        <td> VARCHAR(255)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>operation</td>
        <td>VARCHAR(255)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>status</td>
        <td> INT(11)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>coment</td>
        <td> VARCHAR(255)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>coment_en</td>
        <td> VARCHAR(255)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>description</td>
        <td> VARCHAR(255)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>account_id</td>
        <td> INT(11)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>balance_before</td>
        <td> DECIMAL(19, 4)</td>
        <td> DEFAULT NULL,</td>
        <td> Баланс кошелька до операции</td>
    </tr>
    <tr>
        <td>balance_after</td>
        <td> DECIMAL(19, 4)</td>
        <td> DEFAULT NULL,</td>
        <td> Баланс кошелька после операции</td>
    </tr>
    <tr>
        <td>test_mode</td>
        <td> TINYINT(1)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>initiator_user_id</td>
        <td>INT(11)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>billing_id</td>
        <td> INT(11)</td>
        <td> DEFAULT NULL,</td>
    </tr>
    <tr>
        <td>payment_id</td>
        <td> INT(11)</td>
        <td> DEFAULT NULL,</td>
        <td> Идентификатор из таблицы payments по кторорому производилось начисление</td>
    </tr>
    <tr>
        <td>account_type</td>
        <td> VARCHAR(255)</td>
        <td> NOT NULL,</td>
    </tr>
    <tr>
        <td>currency_id</td>
        <td> INT(11)</td>
        <td> NOT NULL DEFAULT '3',</td>
    </tr>
</table>
