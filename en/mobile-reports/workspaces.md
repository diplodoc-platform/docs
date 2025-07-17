# Workspaces

{% include [note-workspaces](_includes/note-workspaces.md) %}

A workspace is a set of widgets with AppMetrica data. By default, AppMetrica provides access to the main [{{ overview }}](dashboard.md) workspace. In the **Workspaces** section, you can create custom workspaces tailored to your app and each team's needs. You can add a variety of [widgets](widgets.md) to your workspace, reordering them once they're there. Each widget leads to the corresponding report.

{% include notitle [change-workspace](_includes/change-workspace.md) %}

You can [create a new workspace](#create-new) or [copy](#create-copy) and [modify](#edit-workspace) an existing one.

## Creating a workspace {#create-new}

1. In the menu on the left, select **Workspaces**, then click **{{ add-workspace }}** at the bottom.
1. In the window that opens, enter a name for your workspace and click **{{ save }}**.
1. After creating the workspace, you'll see a window where you can add widgets. Select the widgets you need and click **{{ apply }}**.

## Copying a workspace {#create-copy}

{% list tabs %}

- From the workspace list

   1. In the menu on the left, select **Workspaces**.
   1. Find the workspace you want to copy, then click ![](../../_images/dots.svg) → **{{ create-copy }}** on the right.
   1. In the window that opens, enter a name for the new workspace and click **{{ save }}**.

- From a workspace

   1. Open the workspace you want to copy.
   1. In the upper-right corner, click ![](../../_images/dots.svg) → **{{ create-copy }}**.
   1. In the window that opens, enter a name for the new workspace and click **{{ save }}**.

{% endlist %}

You can add both [preset](widgets.md#preset) and [custom](widgets.md#custom) widgets to your workspace. To do that, click **{{ button-add }}** in the upper-right corner.

## Customizing a workspace {#edit-workspace}

You can customize your workspace's look and feel:

- Rearrange widgets.

   {% list tabs %}

   - Drag and drop

      Hover over a widget to see the ![](../../_images/icon-move.svg) icon. Click and hold the icon, then drag the widget to where you want it.

      {% cut "What it looks like" %}

      ![](../../_images/widget-move-line-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

      {% endcut %}

   - Buttons

      Click the up or down arrow on the right of the widget.

      {% cut "What it looks like" %}

      ![](../../_images/widget-move-buttons-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

      {% endcut %}

   {% endlist %}

- Place up to three widgets in a row.

   {% list tabs %}

   - Drag and drop

      Hover over a widget to see the ![](../../_images/icon-move.svg) icon. Click and hold the icon, then drag the widget to where you want it.

      {% cut "What it looks like" %}

      ![](../../_images/widget-move-column-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

      {% endcut %}

   - Button

     Click **+** on the right to add a widget to the group.

      {% cut "What it looks like" %}

      ![](../../_images/widget-add-button-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

      {% endcut %}

   {% endlist %}

- Add titles to organize your widgets into groups.

   {% cut "Widget groups" %}

   ![](../../_images/dashboard-title-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

   {% endcut %}

   To add a title, hover between widgets and click **{{ button-add }}** → **{{ title }}**.

   {% cut "Adding a title" %}

   ![](../../_images/dashboard-add-title-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

   {% endcut %}

## Access rights {#access}

Users with read-only access can create their own workspaces and view those created by others (but they can't edit them).

Users with “Read/edit” access can create, view, and edit any workspace, including those created by others.

## Restrictions {#restrictions}

You can create up to 100 workspaces for a single app. If you have any workspaces that you no longer need, you can delete them.

{% list tabs %}

- From the workspace list

   1. In the menu on the left, select **Workspaces**.
   1. Find the workspace you want to delete, then click ![](../../_images/dots.svg) → **{{ delete }}** on the right.

- From a workspace

   1. Open the workspace you want to delete.
   1. In the upper-right corner, click ![](../../_images/dots.svg) → **{{ delete }}**.

{% endlist %}

One workspace can have up to 100 widgets. To configure their display on the workspace page, use the **{{ widgets }}** button in the upper-right corner.

{% if locale == "ru" %}

## Learn more {#learn-more}

- [Create custom dashboards for your tasks and teams using Workspaces](https://appmetrica.yandex.ru/en/about/blog/workspaces)

{% endif %}

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
