---
title: Communication History
createdAt: 2024-07-08T14:30:56.578Z
updatedAt: 2025-01-23T08:28:29.011Z
---

**The Communication History page** provides users with a comprehensive overview of all data packets exchanged between connectors in the eHub system. It enables users to seamlessly navigate through the history, apply filters to refine searches, export data for further analysis, import new data, and perform actions on specific packets. Additionally, the feature supports customizable views, allowing users to create multiple tabs—each displaying either distinct channel data grids or a unified grid combining multiple channels.


This page also allows users to view and manage PacketTransfer Connectors, which store and organize transmitted data within the eHub system. The stored data is accessible directly from this interface.

Key Components of the Communication History Page:

**Connectors Panel**
Located on the left side, this retractable panel lists all active connectors, categorized by type, making navigation straightforward. Users can switch between connectors easily and choose to pin the panel for constant visibility.

For instance, in this example, two active connectors of type PacketConnector are available: Device01 and Device02. The highlighted connector (Device01) corresponds to the data currently displayed on the page.

**View Tabs**
Positioned at the top, just below the Element Logic navigation bar, these tabs allow users to switch between different views. Views are highly customizable and defined in UIViewConfig.json, specifying how packets appear in table grids. A view can either consolidate all packets into a single grid or separate them by channel into distinct grids.

In this example, three views have been configured:

1. **All**: Displays packets in four distinct table grids:
   - The top-left grid unifies all packets with the channel either "D01 -> D02 Data" or "D02 -> D01 Data".
   - The top-right grid exclusively shows packets of the channel "D02 -> D01 Data".
   - The bottom-left grid exclusively displays "D01 -> D02 Data".
   - The bottom-right grid displays both "D01 -> D02 Ack" and "D02 -> D01 Ack".
2. **Without Ack:** Displays the packets in two table grids:
   - The top grid shows only "D01 -> D02 Data" packets.
   - The bottom grid shows only "D02 -> D01 Data".
3. **Only Sender:** Displays only one table grid containing the packets with the channel "D01 -> D02 Data".

## Filter

The Filter button will prompt a dialog to set the start and end dates/times. After setting parameters, the table grid(s) will display packets within the specified interval.
There is also a advanced filter option. ( to be expanded ) 

To add and document live/ offline mode too

## Actions

The Action button opens a dialog with several options:

### Export

Used to export database packets into a JSON file.

Will prompt another dialog asking to filter the desired packets for exporting. This includes a date/time filter, a checklist of all available channels and the export file name. By default, the date/time filter mirrors the one set on the page, all channels are pre-selected in the checklist, and the file name includes the current date/time and the name of the connector. Upon pressing the Export button, a JSON file containing all packets matching the filter will be downloaded.

### Import

Used to manually introduce packets into the database.

Will request for a JSON file containing the desired packets to be inserted in the database.

### Export Viewer

Used to only view a selected JSON file with packets without adding them in the database.

Will first request for a JSON file containing the desired packets and then enter the page in the Export Viewer mode. In this mode, there will be only one view available, containing all packets, and the possible actions are limited, allowing only packet filtering. Press the Exit Export Viewer button to exit this mode. 

### Manual Stop

This feature is accessible only to users logged in with administrator rights. This forces the completion of an unprocessed packet, marking it with the status ManualStop. This button is disabled if there are no unprocessed packets selected.

### Delete Selected

This feature is accessible only to users logged in with administrator rights. This deletes all currently selected packets from the database.

### Delete All

This feature is accessible only to users logged in with administrator rights. This deletes all packets currently displayed in the packet grid(s).

**Attention**: This action will delete everything filtered by the date/time Filter button. If the packet grid has an advanced filter applied or something in the quick search, even though some packets are hidden, they will still be deleted since they fall within the filter date/time interval.

## Sequence

The Sequence button, available only to administrators, opens a dialog with three options:

- **Sequence Interval:** This action prompts you for a start Id, end Id, and a checklist of channels. It automatically selects everything matching the specified criteria. Use the deselect button to clear all selections.
- **Run Sequence: **Marks the selected packets to be processed again.
- **Delete Sequence:** Deletes the selected packets.

## Autorefresh

When enabled, the page updates automatically when changes occur.

## Lock Scroll

If enabled and multiple table grids are present, scrolling on one grid will synchronize the scroll position across all grids to the closest packets (closest packet Id).

## Packet Data Grid

Depending on the selected view, the page can feature one or multiple table grids, depending on the selected view, displaying transferred packets within the eHub system. Users have several options for interacting with the data:

- **Sorting:** Users can sort this grid on a specific column.
- **Quick Search:** Easily search for a row by entering a value in the Search field; the grid will display only rows containing the introduced value.
- **Advanced Filtering:** Users can apply advanced filters on columns to filter the displayed data.
- **Select: **Users logged in with administrator rights can select packet rows in order to perform actions (run, delete) on them.

The data column will display either the full content of the packet or, based on the configured display format, a dialog button, a preview with a dialog button, or a tree view (used for displaying XMLs or JSONs).

Additionally, on the right side of the data column, the status is displayed. The status can be one of the following:
(Talk to Daniel if here should me some more )
- **Processing:**![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/llGJ6WBXxewnfwhBMxtbG_image.png) Indicates that the packet is currently processing.
- **Error:**![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/FV4GzFBfvtWjeUNlcPxtq_image.png) Signifies that the packet encountered an error during processing. In this case, the packet will attempt to retry processing until it succeeds.
- **Fatal Error:**![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/IZ_JWiOf-hLpmjoUQSSqs_image.png) Indicates a critical error, and the packet will not attempt further retries. The system proceeds to the next packet. If logged in with administrator rights, the users can manually retry the processing of the packet.

If no status is displayed, it means the packet has successfully completed processing.

# Configuration

Each connector has a default view structure that includes two view tabs: "ALL" and "EACH." In the "ALL" view, you'll find a single data grid containing all packets, whereas the "EACH" view provides separate data grids for each distinct channel.

But in order to fully utilise the customisation features, each Connector Project must create a 'UIViewConfig.json' file with the following structure:

```json
```

### Explanations:

Within the "Views" section, you have the flexibility to define as many views as needed. Each view is characterised by the following properties:

- **Name**: A mandatory field representing the view's name;
- **DisplayName**: Translations for the displayed view tab label in multiple languages (the key should be a valid language culture name). If the selected UI language is unspecified in the configuration, or the "DisplayName" property is omitted, the view tab will use the "Name" property as its label;
- **Connectors**: A list of connectors that will show this particular view tab. If not specified, the view will be visible to all connectors. The names of the connectors are defined in the "connectors.json" file;
- **DataDisplayFormat**: Determines how data is presented in the UI inside the channel data grid cell, especially suitable for large data. Can be the following:
  - SingleLine: All data is displayed in a single line, with horizontal scrolling if the data width exceeds the data grid width. This is the default format;
  - MultiLineFull: In case of large data, it's displayed in multiple lines, providing a full view of the content;
  - MultiLineScroll: In case of large data, it's displayed in multiple lines, but with a fixed height determined by a specified number of visible rows, requiring scrolling to view the entire content;
  - Dialog: Only displays a button, and upon clicking it, a pop-up dialog appears, displaying the entire data;
  - XmlFull: If the data is in XML format, it will display it in a tree view format;
  - XmlScroll: If the data is in XML format, it will display it in a tree view format, but with a fixed height determined by a specified number of visible rows, requiring scrolling to view the entire content;
  - XmlDialog: Only displays a button, and upon clicking it, a pop-up dialog appears, displaying the entire XML data;
  - JsonFull: If the data is in JSON format, it will display it in a tree view format;
  - JsonScroll: If the data is in JSON format, it will display it in a tree view format, but with a fixed height determined by a specified number of visible rows, requiring scrolling to view the entire content;
  - JsonDialog: Only displays a button, and upon clicking it, a pop-up dialog appears, displaying the entire JSON data;
- **DataRowCount**: Only relevant when the display format involves scrolling ("MultiLineScroll", "XmlScroll", or "JsonScroll"). It specifies the number of rows visible without scrolling. The default value is set to 1;
- **Channels**: A collection of channel configurations, each of which is displayed as a separate data grid in the UI. These configurations consist of the following properties:
  - **Name**: A mandatory field representing the channel's name;
  - **DisplayName**: Translations for the displayed data grid title in multiple languages (the key should be a valid language culture name). If the selected language is unspecified in the configuration, or the "DisplayName" property is omitted, the data grid will use the "Name" property as its title;
  - **Channel**: Specifies the channel of the packets displayed in this data grid;
  - **DataDisplayFormat**:  Overrides the data format for this specific data grid. Can be omitted to have the display format defined by the parent view;
  - **DataRowCount**: Overrides the row count defined by the parent view for this specific data grid;
  - **Position**: Defines the exact placement of the channel data grid in the UI using row and column indices in a two-dimensional grid layout. When multiple channel data grids share the same row index, they are horizontally aligned in the order of their column index (from left to right). Similarly, when multiple channel data grids share the same column index, they are vertically aligned in the order of their row index (from top to bottom). When multiple channel data grids share the same row index and column index, they merge into a unified data grid, incorporating their respective channels, positioned at the shared indices.

