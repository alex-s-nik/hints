# Действия с ssh

1. Копирование файлов через ssh

   - Директории

      - Windows
   
        ```cmd
        "C:\Program Files\PuTTY\pscp" -r <путь_к_директории> <remote_user>@<remote_host>:<destination_path>
        ```

        Пример
        ```cmd
        "C:\Program Files\PuTTY\pscp" -r c:\projects\nginx root@192.168.1.1:/opt/
        ```

   - Файлы
        - Windows

          ```cmd
          "C:\Program Files\PuTTY\pscp" <путь_к_директории> <remote_user>@<remote_host>:<destination_path>
          ```
        Пример
        ```cmd
        "C:\Program Files\PuTTY\pscp" c:\projects\docker-compose.yaml root@192.168.1.1:/opt/
        ```
