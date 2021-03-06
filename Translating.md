Translations are managed via [Transifex](https://www.transifex.com/team-xonotic/xonotic/dashboard/).

Create an account on Transifex and send a request to join a language team. Once your request has been approved, you can submit suggestions or translations directly through the Transifex interface, or by editing the PO file with an external editor, such as [Poedit](https://poedit.net/) (Transifex allows you to download and upload PO files).

Translations are automatically synced every day from Transifex to the [xonotic-data.pk3dir](https://gitlab.com/xonotic/xonotic-data.pk3dir) git repository and once a week in the opposite direction (may add new translatable strings or change the existing ones).

Translation guidelines and good practices
=========================================
   - [Translation guidelines](Translation-guidelines)
      - [List of translation placeholders](List-of-translation-placeholders)
      - [List of color codes](List-of-color-codes)
      - [List of translation prefixes](List-of-translation-prefixes)

Additional tips
===============
   - [How to test your translations](Test-your-translations)

Implementation notes
====================

Some more technical info is in the data repo: [qcsrc/i18n-guide.txt](https://gitlab.com/xonotic/xonotic-data.pk3dir/blob/master/qcsrc/i18n-guide.txt), [qcsrc/lib/i18n.qh](https://gitlab.com/xonotic/xonotic-data.pk3dir/blob/master/qcsrc/lib/i18n.qh)

Sync is done using a cron job: [misc/infrastructure/transifex.cron](https://gitlab.com/xonotic/xonotic/blob/master/misc/infrastructure/transifex.cron)