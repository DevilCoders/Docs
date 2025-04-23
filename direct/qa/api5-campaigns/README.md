# api5-campaigns
API5: Campaigns

## Возможные ошибки при запуске тестов и их решение

1. Caused by: java.lang.RuntimeException: Failed to init vault client: VAULT_TOKEN environment variable not set

Идем в vault <https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982>, получаем токен к секретнице.
В настройках Run к тесту в Environment variables создаем переменную VAULT_TOKEN и кладем в нее ваш токен секретницы. Чтобы не ошибится с кавычками, лучше делать это через окно Environment Variables, где вводится Name/Value. Есть подробная инструкция здесь https://st.yandex-team.ru/DIRECTKNOL-9 У меня почему-то всё заработало только после того, как я добавил токен в /etc/environment (Linux)

2. Failed to fetch secret ...
javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target

Нужно прописать сертификат YandexInternalCA в Java: https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vjava
В Idea в Build and run выбрать Java, в которой есть сертификат. Поменять "SDK of 'direct-api5-campaigns' module на то, куда указывает $JAVA_HOME

3. javax.xml.ws.WebServiceException: Error while searching for service [javax.xml.ws.spi.Provider]... Caused by: java.lang.ClassNotFoundException: com.sun.xml.internal.bind.v2.ContextFactory

Нужно локально добавить в pom.xml:

        <dependency>
            <groupId>com.sun.xml.ws</groupId>
            <artifactId>jaxws-rt</artifactId>
            <version>2.3.0</version>
        </dependency>

4. Не работает с 11ой Java

Если с 11ой версией Java не работает, то возможно нужно пробовать 8ую либо 12ую (кажется есть какой-то артефакт джарниковский, который собран под 8-ой и под 12-ой)
