
<script>
	let done;
</script>

<div class="settings">
	<div class="top"></div>
	<div class="nav">
		<h4>Перейти к настройкам:</h4>
		<ul>
			<li><a href="http://192.168.1.1/#pswd">Пароль контроллера</a></li>
			<li><a href="http://192.168.1.1/#readers">Считыватели</a></li>
			<li><a href="http://192.168.1.1/#lock">Замок</a></li>
			<li><a href="http://192.168.1.1/#drive">Привод двери</a></li>
			<li><a href="http://192.168.1.1/#tamper">Датчик вскрытия корпуса</a></li>
			<li><a href="http://192.168.1.1/#entry-sensors">Датчики прохода</a></li>
			<li><a href="http://192.168.1.1/#alarm">Сигнализация</a></li>
			<li><a href="http://192.168.1.1/#auth">Авторизация</a></li>
			<li><a href="http://192.168.1.1/#network">Сеть</a></li>
			<li><a href="http://192.168.1.1/#time-sync">Сервер синхронизации времени</a></li>
			<li><a href="http://192.168.1.1/#mqtt">MQTT</a></li>
			<li><a href="http://192.168.1.1/#modbus">Modbus</a></li>
			<li><a href="http://192.168.1.1/#integration">Интеграции</a></li>
			<li><a href="http://192.168.1.1/#power-supply">Блок питания</a></li>
			<li><a href="http://192.168.1.1/#door-events">События двери</a></li>
		</ul>
	</div>
	<div class="a"> <button class="a_save">Применить настройки</button> <button class="a_rst">Сбросить настройки</button> <button class="a_downl">Скачать настройки</button> </div>
	<div class="s">
		<div class="s_g" id="save-load">
			<h4>Загрузка настроек из .josn файла</h4> <input type="file" id="settings"> <button class="a_load">Загрузить настройки</button>
		</div>
		<h4>Изменить настройки контроллера:</h4>
		<div class="s_g" id="pswd">
			<h4>Изменить пароль</h4> [1] Пароль <input type="password" name="controllerPassword">
		</div>
		<div class="s_g" id="readers">
			<h4>Считыватели</h4> [2] Считыватель на вход <select name="readerInEnable">
				<option value="0">Выключен</option>
				<option value="1">Wiegand</option>
				<option value="2">Touch memory</option>
				<option value="3">OSDP</option>
			</select> [3] Считыватель на выход <select name="readerOutEnable">
				<option value="0">Выключен</option>
				<option value="1">Wiegand</option>
				<option value="2">Touch memory</option>
				<option value="3">OSDP</option>
			</select> <label>[4] Проверка контрольной суммы Touch Memory <input type="checkbox" name="verifyTouchMemCheckSum"></label> <label>[5] Проверка битов четности Wiegand <input type="checkbox" name="verifyWiegandBitsParity"></label> [66] Скорость последовательной передачи OSDP <select name="osdpSerialBaudRate">
				<option value="9600">9600 бод</option>
				<option value="19200">19200 бод</option>
				<option value="38400">38400 бод</option>
				<option value="57600">57600 бод</option>
				<option value="115200">115200 бод</option>
			</select> <label>[67] Базовый ключ защищенного канала OSDP на вход (HEX длиной 32 без пробелов) <input name="secureChannelBaseKeyOsdpIn"></label> <label>[68] Базовый ключ защищенного канала OSDP на выход (HEX длиной 32 без пробелов) <input name="secureChannelBaseKeyOsdpOut"></label> [69] Адрес контроллера в сети OSDP IN <input type="number" min="0" max="255" name="addressOsdpIn"> [70] Адрес контроллера в сети OSDP OUT <input type="number" min="0" max="255" name="addressOsdpOut">
		</div>
		<div class="s_g" id="lock">
			<h4>Замок</h4> <label>[6] Вход чтения состояния язычка <input type="checkbox" name="tonguePinEnable"></label> <label>[7] Вход чтения состояния ригеля <input type="checkbox" name="rigelPinEnable"></label> <label>[8] Вход чтения состояния ручки <input type="checkbox" name="handlePinEnable"></label> <label>[9] Вход чтения состояния цилиндра <input type="checkbox" name="cylinderPinEnable"></label> <label>[10] Вход чтения состояния саботажа <input type="checkbox" name="sabotagePinEnable"></label> [11] Тип сигнала реле 1 для управления замком <select name="lockRelaySignalType">
				<option value="0">Постоянный сигнал</option>
				<option value="1">Импульс</option>
			</select> [12] Состояние замка при активации реле постоянным сигналом <select name="lockStateAtRelayConstSignal">
				<option value="0">Закрыт</option>
				<option value="1">Открыт</option>
			</select> [13] Время импульса реле 1 для управления замком <input type="number" name="lockRelayPulseTime"> [14] Задержка запирания замка после закрытия двери <input type="number" name="delayDoorLock">
		</div>
		<div class="s_g" id="drive">
			<h4>Привод</h4> 
      [15] Подключен ли привод <select name="doorDriveEnable" bind:value={done}> 
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select>
      {#if done === "true"}
        [16] Время импульса реле 2 для управления приводом <input type="number" name="driveRelayPulseTime"> [17] Задержка активации привода при открытии замка (время выдвижения ригелей) <input type="number" name="delayDriveActivation">
      {/if}
      </div>
		<div class="s_g" id="tamper">
			<h4>Датчик вскрытия корпуса</h4> [18] Активировать датчик вскрытия корпуса <select name="temperSensorEnable">
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select> [19] Время активного сигнала датчика вскрытия корпуса для регистрации события <input type="number" name="temperSensorActiveSignalTimeForEventReg">
		</div>
		<div class="s_g" id="entry-sensors">
			<h4>Датчики прохода</h4> [20] Подключены ли датчики прохода <select name="entrySensorsEnable">
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select> [21] Время активного сигнала датчика прохода для регистрации события <input type="number" name="entrySensorActiveSignalTimeForEventReg">
		</div>
		<div class="s_g" id="alarm">
			<h4>Сигнализация</h4> [22] Активировать контакты сигнализации (ALARM) <select name="alarmLineEnable">
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select> [23] Время активного сигнала для срабатывания сигнализации <input type="number" name="activeSignalTimeForAlarmActivation">
		</div>
		<div class="s_g" id="auth">
			<h4>Авторизация</h4> [24] Время удержания двери в открытом положении после успешной авторизации <input type="number" name="doorHoldTimeAfterAuth"> [25] Список событий для старта авторизации на входе <div class="lg"> <label>• Запрос входа <input type="checkbox" name="auth_act_in_4"></label> <label>• Найдено лицо <input type="checkbox" name="auth_act_in_1"></label> <label>• Датчик прохода активировался <input type="checkbox" name="auth_act_in_5"></label> <label>• Считыватель отправил ключ <input type="checkbox" name="auth_act_in_2"></label> </div> [26] Список этапов авторизации на входе <div class="lg"> <label>• Считыватель отправил ключ <input type="checkbox" name="auth_ast_in_2"></label> <label>• Лицо распознано <input type="checkbox" name="auth_ast_in_1"></label> <label>• Доступ по QR <input type="checkbox" name="auth_ast_in_6"></label> <label>• Подтверждение доступа <input type="checkbox" name="auth_ast_in_3"></label> <label>• Мобильное приложение <input type="checkbox" name="auth_ast_in_0"></label> </div> [27] Список событий для старта авторизации на выходе <div class="lg"> <label>• Запрос входа <input type="checkbox" name="auth_act_out_4"></label> <label>• Найдено лицо <input type="checkbox" name="auth_act_out_1"></label> <label>• Датчик прохода активировался <input type="checkbox" name="auth_act_out_5"></label> <label>• Считыватель отправил ключ <input type="checkbox" name="auth_act_out_2"></label> </div> [28] Список этапов авторизации на выходе <div class="lg"> <label>• Считыватель отправил ключ <input type="checkbox" name="auth_ast_out_2"></label> <label>• Лицо распознано <input type="checkbox" name="auth_ast_out_1"></label> <label>• Доступ по QR <input type="checkbox" name="auth_ast_out_6"></label> <label>• Подтверждение доступа <input type="checkbox" name="auth_ast_out_3"></label> <label>• Мобильное приложение <input type="checkbox" name="auth_ast_out_0"></label> </div> [29] Максимальное время авторизации <input type="number" name="maxAuthTime">
		</div>
		<div class="s_g" id="network">
			<h4>Сеть</h4> [38] Подключение к сети <select name="networkConnection">
				<option value="0">Ethernet DHCP</option>
				<option value="1">Ethernet (Статический IP-адрес)</option>
				<option value="2">Wi-Fi</option>
			</select> [39] MAC адрес <input name="macAddress"> [40] Название точки доступа Wi-Fi <input name="wifiSSID"> [41] Настройка пароля Wi-Fi <input name="wifiPassword"> [42] Стандарт безопасности WIFI <select name="wifiSecurityStandart">
				<option value="2">WPA PSK</option>
				<option value="3">WPA2 PSK</option>
				<option value="4">WPA/WPA2 PSK</option>
				<option value="6">WPA3 PSK</option>
			</select> [43] IP-адрес <input name="ipAddress"> [44] Маска сети <input name="networkMask"> [45] Шлюз по умолчанию <input name="defaultGateway">
		</div>
		<div class="s_g" id="time-sync">
			<h4>Сервер синхронизации времени</h4> [46] Адрес сервера синхронизации времени 1 <input name="timeSyncServerAddress1"> [47] Адрес сервера синхронизации времени 2 <input name="timeSyncServerAddress2"> [48] Адрес сервера синхронизации времени 3 <input name="timeSyncServerAddress3"> [49] Интервал синхронизации времени (в минутах) <input type="number" min="1" name="timeSyncInterval">
		</div>
		<div class="s_g" id="mqtt">
			<h4>MQTT</h4> [50] Включение протокола SSL для MQTT <select name="mqttSslEnable">
				<option value="false">Выключен</option>
				<option value="true">Включен</option>
			</select> [51] SSL сертификат сервера (pem) <textarea name="mqttServerSslCert" cols="70" rows="20"></textarea> [52] SSL сертификат клиента (crt) <textarea name="mqttClientSslCert" cols="70" rows="20"></textarea> [53] SSL приватный ключ клиента (key) <textarea name="mqttClientSslPrivateKey" cols="70" rows="20"></textarea> [54] Адрес MQTT брокера <input name="mqttBrokerAddress"> [55] Имя пользователя MQTT <input name="mqttUsername"> [56] Пароль пользователя MQTT <input name="mqttPassword"> [57] Временной интервал для контроля отключения от брокера (KeepAlive) <input type="number" min="0" name="mqttKeepAliveTime"> [58] Уровень качества обслуживания (QoS) <select name="mqttQos">
				<option value="0">0</option>
				<option value="1">1</option>
				<option value="2">2</option>
			</select>
		</div>
		<div class="s_g" id="modbus">
			<h4>Modbus</h4> [59] Активировать обработчик Modbus <select name="handlerModbusEnable">
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select> [60] Адрес контроллера в сети Modbus <input type="number" min="0" max="247" name="controllerAddressInModbusNetwork"> [61] Скорость последовательной передачи Modbus <select name="modbusSerialBaudRate">
				<option value="9600">9600 бод</option>
				<option value="19200">19200 бод</option>
				<option value="38400">38400 бод</option>
				<option value="57600">57600 бод</option>
				<option value="115200">115200 бод</option>
			</select>
		</div>
		<div class="s_g" id="integration">
			<h4>Интеграции</h4> [62] Активировать контакты для интеграции <select name="integrationContactsEnable">
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select> [63] Длительность импульса (мс) для срабатывания входов интеграции <input type="number" name="activeSignalTimeForIntegrationInputActivation">
		</div>
		<div class="s_g" id="power-supply">
			<h4>Блок питания</h4> [64] Проверка состояния блока питания на отсутствие напряжения сети <select name="checkingPowerSupplyForNoMainsVoltage">
				<option value="false">Выключена</option>
				<option value="true">Включена</option>
			</select>
		</div>
		<div class="s_g" id="door-events">
			<h4>События двери</h4> [65] Регистрировать событие “Проход без авторизации” <select name="registerEntryWithoutAuth">
				<option value="false">Нет</option>
				<option value="true">Да</option>
			</select>
		</div>
		<div class="s_g" id="firmware-update">
			<h4>Обновление прошивки</h4> <input type="file" id="firmware"> <button class="a_flash">Обновить прошивку</button>
		</div>
	</div>
	<div class="a"> <button class="a_save">Применить настройки</button> <button class="a_rst">Сбросить настройки</button> <button class="a_downl">Скачать настройки</button> </div>
	<div id="bottom"></div>
	<div class="nav-btns"> <a href="http://192.168.1.1/#top"><button class="nav_btn">↑</button></a> <a href="http://192.168.1.1/#bottom"><button class="nav_btn">↓</button></a> </div>
</div>

<style>
	.s {
		margin: 10px 0px;
		max-width: 700px;
	}

	.s_g {
		padding: 20px;
		margin-top: 10px;
		border: 1px solid black;
	}

	.s_g:nth-child(odd) {
		background-color: #f5f5f5;
	}

	input,
	select,
	textarea,
	label {
		margin-top: 5px;
		margin-bottom: 10px;
		display: block;
		padding: 5px;
	}

	label {
		padding: 0px;
	}

	input[type="checkbox"] {
		display: inline-block;
	}

	button {
		padding: 5px;
	}

	h4 {
		margin: 0 0 10px 0;
	}

	.lg {
		margin-bottom: 10px;
	}

	.lg label {
		margin: 0 0 0 30px;
	}

	.nav-btns {
		position: fixed;
		right: 0px;
		bottom: 0px;
		display: flex;
	}

	.nav_btn {
		width: 50px;
		height: 50px;
		border: 0;
		margin-left: 5px;
		font-size: 22px;
		font-weight: 600;
	}
	</style>