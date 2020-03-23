# How to add new frontend localization via admin UI

1. In VC Platform go to ->Stores module->Select the ODT store;

1. Under additional languages select de-DE and save the changes by clicking the 'Save' button;

1. Go to Content module->select the ODT store-> select Themes in ODT store->select the 'Default'  theme;

1. In the opened blade (Manage theme assets)  select the 'locales 'folder;

1. Upload the new locale file to 'locale' folder in the theme using an appropriate name (ex., 'de.json');

1. **Important!** The file should be prepared in advance:

     1. Download the en.default.json in 'locales' folder;

     1. Translate the terms into the desired language in the json file;

     1. Saved locally on PC.

1. Restart the Storefront;

1. Go to ODT URL with local segment adding (ex, https://dev-odt-public.azurewebsites.net/de-DE/). 