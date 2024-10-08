+++
# vim:formatoptions=tj
# vim:textwidth=100
title = "В поисках дзена: Merge vs. Rebase"
date = 2024-08-18

[taxonomies]
tags=["git"]

[extra]
repo_view = true
+++

TOC:

- основы гита;
- про мерж (сквош, мерж и ребаза);
- хуки (?)

## Введение

Привет!

Меня зовут Матвей, я занимаюсь Front-end разработкой. Вот уже на протяжении 4 лет я каждый день
использую систему контроля версий (англ. VCS - version system control), в частности git.

Все мы прекрасно понимаем важность и необходимость в использовании данного инструмента при
совместной разработке. Один из больших плюсов Git является тот факт, что исходный код хранится не на
единой машине (центральном сервере). Вместо этого он работает полностью локально, сохраняя все
необходимые данные на вашей персональной машине. Данная директория называется репозиторием. Его
можно синхронизировать с удаленным сервером, что позволяет нескольким людям одновременно работать
над одним и тем же проектом и изменять одни и те же файлы. Частным примером подобных сервисов по
хранению репозиториев являются GitHub, Bitbucket и GitLab, а также многие другие.

В данной статье я бы хотел вам рассказать о таких способах ведения истории измениний, как rebase и
merge. Мы познакомимся с каждым из них подробнее, рассмотрим их плюсы и минусы, а также разберемся,
в какой ситуации предпочтительней тот или иной метод. Давайте приступим!

## Git Rebase: Переписываем историю

Git rebase - это мощная команда, которая позволяет **переписать историю коммитов** вашей ветки.

**Как работает `rebase`?**

Вместо того, чтобы просто объединять (merge) ветку с другой, `rebase` переносит все изменения из
одной ветки на другую, как будто они были сделаны непосредственно на целевой ветке
**в хронологическом порядке**.

**Преимущества использования `rebase`:**

- **Чистая история**:
  - `Rebase` помогает сохранить историю коммитов линейной и понятной.
  - Это полезно для удаления промежуточных шагов или исправления ошибок в прошлых коммитах.
- **Обновление ветки**:
  - `Rebase` позволяет легко обновить локальную ветку до последней версии целевой ветки перед
    созданием новых коммитов.

**Пример использования:**

1. Вы работаете над новой функцией в ветке `feature`.
2. Во время вашей работы, Ваш коллега внес правки по критичному bug-fix в репозиторий.
3. Теперь Вам необходимо получить последние правки и интегрировать их со своей локальной веткой
   `feature`. Вместо объединения (`merge`), вы можете использовать `rebase`:

<center>
    <img src="./git-rebase--before.svg" alt="История коммитов до выполнения `git rebase`" />
</center>

```bash
git rebase origin main
```

где `origin` - название удаленного репозитория.

- `git rebase feature`: переносит все изменения из ветки `feature` на `main`.

<center>
    <img src="./git-rebase--after.svg" alt="История коммитов после выполнения `git rebase`" />
</center>

**Важно знать:**

- **Изменения в истории**: `Rebase` изменяет историю коммитов.
- **Совместная работа**: Используйте `rebase` с осторожностью, если вы работаете над проектом с
  другими разработчиками.
- **Предварительная проверка**: Перед использованием `rebase` убедитесь, что вы понимаете его
  последствия.

Git `rebase` - это мощный инструмент, который может быть полезен для управления историей коммитов и
поддержания чистой ветвления в вашем проекте Git.

**Дополнительные ресурсы:**

- [Документация git](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) -
- [Tutorial от Atlassian](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)
