## ssqls-hierarchy

ssqls-hierarchy -- утилита для создания графа зависимостей ssqls-файлов в формате *.gv (для graphviz)

Использование:

    Create hierarchy graph from *.ssqls file [-h] [-O [OUTPUT_FILE]] -S
                                                    SOURCE_ROOT [-B [BASE_DIR]]
                                                    path
    
    positional arguments:
      path                  Path to ssqls file
    
    optional arguments:
      -h, --help            show this help message and exit
      -O [OUTPUT_FILE], --output-file [OUTPUT_FILE]
                            Path to resulting graph. By default "<input-file>.gv"
                            will be used.
      -S SOURCE_ROOT, --source-root SOURCE_ROOT
                            Path to arcadia dir
      -B [BASE_DIR], --base-dir [BASE_DIR]
                            Base dir for construct relative paths to ssqls. By
                            default source-root will be used.

Для для просмотра результатов работы утилиты рекомендуется использовать пакет graphviz
https://graphviz.gitlab.io/

Установка graphviz:

    sudo apt install graphviz

Рендер картинки с иерархией:

    dot -Tpng -o <output-file.png> <input-file.ssqls.gv>
