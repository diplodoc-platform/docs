# Публикация на GitHub Pages

1. В GitHub в репозитории вашего документа перейдите на вкладку **Settings**  и в меню слева выберите **Pages**.

1. В разделе **Build and deployment** в выпадающем списке выберите **GitHub Actions** и в появившемся блоке **Static HTML** нажмите кнопку **Configure**.  Откроется окно редактирования экшна.

1. В блоке `jobs` после строки `uses: actions/configure-pages@v5` добавьте код

    ```yaml
    - name: Build docs
      uses: diplodoc-platform/docs-build-action@v3
      with:
        src-root: './docs'
        build-root: './docs-html'
    ```

1. Вверху справа нажмите **Commit changes...**, укажите имя коммита в поле **Commit message** и нажмите кнопку **Commit changes**.

1. Перейдите на вкладку **Actions**. Вверху списка будет ваш последний коммит. 

1. Нажмите на название коммита. После завершения сборки, документ будет размещен на GitHub Pages. Посмотреть его можно по ссылке ниже под надписью **deploy**.