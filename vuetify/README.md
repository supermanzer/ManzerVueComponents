# Vuetify Components

These components are based on the Vuetify.js material design UI library.

## Contents

- **tables**

  1. **ServerSideDataTable**: A version of the Vuetify data table that assumes searching, sorting, and pagination occurs on the server side. Rather than perform any updates to the table directly, it emits the `options` object which contains the parameters for sorting & pagingation that the user may have triggered. It also hides the default Vuetify data table footer and repalces it with a pagination component. A parent component can listen for the emitted event and trigger whatever API request is appropriate.

     **Slots**

     - `table-top`: A slot for creating a custom header within the table (I use this for a title and Search features)
     - `table-actions`: This is a slot on each item at the right end of the table. As it's utility is for read, update, and delete type actions it binds the `{item}` object in the `slotProps`.

     **Props**

     - `headers`: Table headers. Defines the columns and their names. [See example](https://vuetifyjs.com/en/api/v-data-table/#headers)
     - `records`: Table data
     - `pageCount`: Total number of pages in paginated data source.
     - `noDataText`: Text that will be rendered in table body if `records.length === 0`

- **buttons**

  1. **InfoIconDialog**: A button that loads [@nuxt/content](https://content.nuxtjs.org/) content into a dialog (modal) window and displays it to the user. I find this useful to create in-app documentation and help articles. _This assumes the project is utilizing the Nuxt,js content module_. I do not use the `asyncData` approach in this component since I'm using props to define what content to render and need access to `this`.

     **Slots**

     - `card-title`: Allows for more customization of the card title in the dialog

     **Props**

     - `width`: Define the width of the dialog window rendered (defaults to 500px).
     - `icon`: Define the icon rendered in the initial button (defaults to information-outline)
     - `tooltip_text`: The text rendered in the tooltip (defaults to 'Click for Info')
     - `title_text`: The text rendered in the card title (defaults to 'Information')
     - `path`: File path in `content` directory to the article we wish to display (defaults to 'info')
     - `document`: The actual markdown document we want rendered in the dialog (_requred_)
