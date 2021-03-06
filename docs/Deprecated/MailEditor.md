## Mail Editor

## Deprecated!
**Warning!** This feature has been deprecated within version 3.3. 
It still will be available for BC reasons but is not recommended anymore.
Please use the mail layout editor module in [Email Channel](../OutputWorkflow/10_EmailChannel.md) within the [Output Workflows](../OutputWorkflow/0_Usage.md) instead.

***

![](http://g.recordit.co/OJ7uM6FxY0.gif)

> **Attention**: This mail editor does not respect any special mail template language (like inky)!
 
## Things to know
- Always save your form before opening the mail editor
- The mail editor is locale aware. However, there is a `default` row which will be used, if no localized data is available

## Custom Service
Use the mail editor to specify some special mail templates.
It's very easy to add some custom template widgets (Eg. date field).

### Register Service:
```yml
AppBundle\MailEditor\Widget\SpecialWidget:
    tags:
        - { name: form_builder.mail_editor.widget, type: special }
```

### Add PHP Service:
```php
<?php

namespace AppBundle\MailEditor\Widget;

use FormBuilderBundle\MailEditor\Widget\MailEditorWidgetInterface;

class DateWidget implements MailEditorWidgetInterface
{
    public function getWidgetGroupName()
    {
        return 'form_builder.mail_editor.widget_provider.others';
    }

    public function getWidgetLabel()
    {
        return 'form_builder.mail_editor.widget_provider.special.label';
    }

    public function getWidgetConfig()
    {
        // this config will appear in the editor if you double-click on your widget
        return [
            'link' => [
                'type'         => 'input',
                'defaultValue' => null,
                'label'        => 'form_builder.mail_editor.widget_provider.special.link'
            ],
        ];
    }

    public function getValueForOutput(array $config)
    {
        $form = $config['form'];
        $link = isset($config['link']) ? $config['link'] : '';

        return 'SPECIAL_DATA';
    }
}
```