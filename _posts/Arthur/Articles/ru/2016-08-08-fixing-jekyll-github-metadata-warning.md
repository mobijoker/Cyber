---
title: Как исправить предупреждение о Jekyll + GitHub Metadata
ref: fixing-jekyll-github-metadata-warning
permalink: /ru/web/fixing-jekyll-github-metadata-warning.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - web
tags:
  - jekyl
  - github pages
  - error
  - warning
  - github metadata
  - github API authentication
  - github token
  - JEKYLL_GITHUB_TOKEN

---

![thumb](/images/fixing-jekyll-github-metadata-warning/error.png)
Когда Я использую `jekyll serve` команду в моём локальном Jekyll окружении Я получаю следующее предупреждение:
<pre>
GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.
</pre>

<br>

Здесь объяснение того, как исправить эту ошибку:


**Шаг 1.** Создай персональный токен доступа GitHub с `public_repo` scope. Ты можешь найти руководство здесь [here](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).

![](/images/fixing-jekyll-github-metadata-warning/github-metadata-error.png)

> **Примечание:** Помни о том чтобы держать ключ в секрете - ведь ты же не хочешь чтобы другие люди использовали API от твоего имени!


<br>
**Шаг 2.** Открой `~/.bash_profile` файл (ты можешь использовать твой любимый текстовый редактор вместо `nano`).

```sh
nano ~/.bash_profile
```

> **Примечание:** Этот фаил может иметь различные имена и места расположения в зависимости от используемых shell и OS. Например: `.profile`, `.bashrc`, `.zshenv`. В MacOS это `.bash_profile` который расположен в пользовательской домашней дирректории (`~/`). Ты можешь найти в Google информацию о файле в которой ты можешь добавить новую переменную окружения именно для твоей OS.


<br>
**Шаг 3.** Затем определите новую переменную окружения с именем переменной `JEKYLL_GITHUB_TOKEN` и токен доступа GitHub как значение переменной (которое что-то вроде `abc123def456`). Ты можешь сделать это добавив следующую строку в конец файла:

```
export JEKYLL_GITHUB_TOKEN='abc123def456'
```

> **Примечание:** Замени `abc123def456` на твой токен.


<br>
**Шаг 4.** Теперь перезагрузи терминал.

Ты можешь проверить новую переменную окружения со следующей командной строкой, которая должна отобразить твой GitHub токен.

```sh
echo $JEKYLL_GITHUB_TOKEN
```


### В дополнение

По соображениям безопасности ты можешь также получить доступ к GitHub токену со следующей командной строкой при постройке или администрировании веб-сайта на Jekyll:

```sh
JEKYLL_GITHUB_TOKEN=abc123def456 bundle exec jekyll serve
```

Также ты можешь установить временную переменную окружения с помощью следующей командной строки:

```sh
export JEKYLL_GITHUB_TOKEN=abc123def456
```

Комманда `export` запускаемая самостоятельно, а не из `.bash_profile` файла будет только временной настройкой и переменная окружения будет существовать только до перезагрузки.
