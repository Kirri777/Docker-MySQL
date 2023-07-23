# Docker + MariaDB + PhpMyAdmin

## Links

http://127.0.0.1:81/ - PhpMyAdmin (`PHPMYADMIN_80` in `.env` config)

<br />

## Installation

1. Download folder.

2. Create the file `./.docker/.env` using `./.docker/.env.example` as template.<br />
    For multiple dockers you need change every time `COMPOSE_PROJECT_NAME` and `port` variables.

3. Go inside folder `./docker` and run `docker-compose up -d --build` to start containers.

<br />

## Change timezone

1. To check current time:

    ```sql
    SELECT now();
    ```

2. The current global and session time zone values can be retrieved like this:

    ```sql
    SELECT @@GLOBAL.time_zone, @@SESSION.time_zone;
    ```
    
    - As the value 'SYSTEM', indicating that the server time zone is the same as the system time zone.
    - As a string indicating an offset from UTC of the form [H]H:MM, prefixed with a + or -, such as '+10:00', '-6:00', or '+05:30'. A leading zero can optionally be used for hours values less than 10; MySQL prepends a leading zero when storing and retrieving the value in such cases. MySQL converts '-00:00' or '-0:00' to '+00:00'.
    Prior to MySQL 8.0.19, this value had to be in the range '-12:59' to '+13:00', inclusive; beginning with MySQL 8.0.19, the permitted range is '-13:59' to '+14:00', inclusive.
    - As a named time zone, such as 'Europe/Helsinki', 'US/Eastern', 'MET', or 'UTC'.
    - Named time zones can be used only if the time zone information tables in the mysql database have been created and populated. Otherwise, use of a named time zone results in an error:
    <br />

    ```sql
    mysql> SET time_zone = 'UTC';
    ERROR 1298 (HY000): Unknown or incorrect time zone: 'UTC'
    ```
    
3. To change timezone, you need set this value in sql:

    ```sql
    SET time_zone = 'Europe/Warsaw';
    SET GLOBAL time_zone = 'Europe/Warsaw';
    ```

<br />

## Problems

1. Problem

    ```
    Error during session start; please check your PHP and/or webserver log file and configure your PHP installation properly. Also ensure that cookies are enabled in your browser.

    session_start(): open(SESSION_FILE, O_RDWR) failed: Permission denied (13)

    session_start(): Failed to read session data: files (path: /sessions)
    ```

    To fix the problem, you need to add both 777 permissions and root ownership to the sessions folder.

    Here's how you can do it:

    1. Open a terminal or command prompt on a container and navigate to the `/` folder.

    2. Run the following command to change the ownership to root:

        ```
        chown root sessions
        ```

        This command changes the owner of the sessions folder to root.

    3. Run the following command to add 777 permissions:

        ```
        chmod 777 sessions
        ```

        This command grants read, write, and execute permissions to all users for the sessions folder.