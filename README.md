---
title: Communication History
createdAt: 2024-07-08T14:30:56.578Z
updatedAt: 2025-01-23T08:28:29.011Z
---

**The Communication History page** provides users with a comprehensive overview of all data packets exchanged between connectors in the eHub system. It enables users to seamlessly navigate through the history, apply filters to refine searches, export data for further analysis, import new data, and perform actions on specific packets. Additionally, the feature supports customizable views, allowing users to create multiple tabs—each displaying either distinct channel data grids or a unified grid combining multiple channels.

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/HistoryUI.png)

This page also allows users to view and manage PacketTransfer Connectors, which store and organize transmitted data within the eHub system. The stored data is accessible directly from this interface.

Key Components of the Communication History Page:

**Connectors Panel**
Located on the left side, this retractable panel lists all active connectors, categorized by type, making navigation straightforward. Users can switch between connectors easily and choose to pin the panel for constant visibility.

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/ConnectorsPanel.png)

For instance, in this example, two active connectors of type PacketConnector are available: Device01 and Device02. The highlighted connector (Device01) corresponds to the data currently displayed on the page.

## View Tabs
Positioned at the top, just below the Element Logic navigation bar, these tabs allow users to switch between different views. Views are highly customizable and defined in UIViewConfig.json, specifying how packets appear in table grids. A view can either consolidate all packets into a single grid or separate them by channel into distinct grids.

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/Alle.png)
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/All-in-One.png)
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/DataOnly.png)

In this example, three views have been configured:

1. **All**: Displays packets in four distinct table grids:
   - The top-left grid exclusively shows packets of the channel "D01 -> D02 Data".
   - The top-right grid exclusively shows packets of the channel "D02 -> D01 Data".
   - The bottom-left grid displays both "D01 -> D02 Errors" and "D02 -> D01 Errors".
   - The bottom-right grid displays both "D01 -> D02 Ack" and "D02 -> D01 Ack".
2. **All-in-One:** Displays a single grid that contains the packets from all existing channels".
3. **Data Only:** Displays the packets in two table grids:
   - The left grid shows only "D01 -> D02 Data" packets.
   - The right grid shows only "D02 -> D01 Data" packets.


## Filter

The Filter button will prompt a dialog to set the start and end dates/times. After setting parameters, the table grid(s) will display packets within the specified interval.

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/Filter.png)
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/Filterdialog1.png)
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/FilterDialog2.png)

### Extended Feature: Advanced Filter

The **Advanced Filter** feature provides a more flexible way to filter data beyond the standard date and time filtering. It allows users to define multiple conditions across different columns in the data table.

This option is located at the bottom of the standard filter dialog. 

- **Advanced Filter Dialog**
  ![Advanced Filter Button](https://raw.githubusercontent.com/Trefla25/UIDoc/main/AdvancedFilter.png)

#### How It Works

1. **Column Selection**  
   - Users can select any column from the dataset to apply filtering.  
   - The dropdown displays all available columns in the table.
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/AdvancedFilterDialog.png)

2. **Operator Selection**  
   - After selecting a column, the user must choose an appropriate operator based on the data type of that column.  
   - Example:
     - Numeric columns (e.g., `Id`) support operators such as `>`, `<`, `=`, etc.
     - Text-based columns (e.g., `Data`) support operators like `contains`, `equals`, etc.

3. **Defining the Filter Condition**  
   - Once the column and operator are set, the user can input a specific value for filtering.  
   - The filter will apply only after all required selections are made.

4. **Adding Multiple Filters**  
   - Users can add multiple filtering conditions either for different columns or apply multiple conditions on the same column.  
   - Clicking the **"Add Column Filter"** button adds a new row, allowing additional filter criteria to be set.

5. **Managing Filters**  
   - Users can remove an applied filter by clicking the delete (🗑) button next to the filter row.  
   - The **Cancel** button discards changes, while the **Ok** button applies the filters to the table.

This feature enhances data filtering by giving users more granular control over how data is displayed, making it easier to refine search results based on specific conditions.

## Actions

The Action button opens a dialog with several options:

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/Actions.png)
### Export

Used to export database packets into a JSON file.

Will prompt another dialog asking to filter the desired packets for exporting. This includes a date/time filter, a checklist of all available channels and the export file name. By default, the date/time filter mirrors the one set on the page, all channels are pre-selected in the checklist, and the file name includes the current date/time and the name of the connector. Upon pressing the Export button, a JSON file containing all packets matching the filter will be downloaded.

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/Export.png)
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/ExportDropdown.png)
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

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/Sequence.png)

- **Sequence Interval:** This action prompts you for a start Id, end Id, and a checklist of channels. It automatically selects everything matching the specified criteria. Use the deselect button to clear all selections.
- **Run Sequence: **Marks the selected packets to be processed again.
- **Delete Sequence:** Deletes the selected packets.

## Live/Offline Mode

The **Live/Offline Mode** toggle allows users to switch between a dynamic real-time packet view and a historical packet view with pagination. This feature optimizes performance and ensures smooth UI operation by managing packet loading efficiently.

### Live Mode

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/LiveMode.png)

- **Dynamic, real-time view**  
  In **Live Mode**, users can see only the **last X packets** that were sent to the UI, where **X is a configurable value** set in a JSON configuration file.
- **Automatic updates**  
  This mode updates and refreshes constantly as new packets arrive, displaying only the most recent packets based on their creation timestamp.
- **Scrollable table**  
  Since this mode focuses only on the latest packets, the view is a **scrollable table** instead of paginated.

### Offline Mode

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/OfflineMode.png)

- **Full packet history**  
  In **Offline Mode**, users can view **all packets ever sent** (within the range of the applied date-time filter).
- **Paginated view**  
  Unlike Live Mode, where the table is scrollable, **Offline Mode uses pagination**. The number of packets displayed per page is the same **X value from the configuration JSON file**.
- **Progressive loading for better performance**  
  When switching to **Offline Mode**, packets load in increments of **X packets per page**. Initially, only the first page with **X packets** is shown, and additional packets load progressively, improving performance and responsiveness.

  ![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/OfflinePagination.png)

### Shared Behavior Across Modes

- **Changes apply to both modes**  
  Any action performed in one mode (e.g., deleting a packet) will reflect in both modes and the entire system.
- **Performance optimization**  
  The **Live/Offline Mode** ensures smooth packet handling, reducing unnecessary memory usage while allowing efficient packet retrieval and display.

This feature improves performance and makes the UI more responsive, ensuring a seamless experience when handling real-time and historical data.

## Group Packets

The **Group Packets** switch allows users to toggle between **grouped** and **individual** packet display modes. This feature enhances data organization by structuring related packets into parent-child relationships.

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/GroupPackets.png)

- The **Group Packets** switch is located in the UI near the **Live Mode toggle**.
- Users can **toggle this setting on or off at any time** to adjust how packets are displayed.

### Grouped Packets Mode (Enabled)

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/GroupedPackets.png)

- When **Group Packets** is **enabled**, packets are displayed in **parent-child groups**.
- A **parent packet** can have **multiple child packets**.
- Users can **expand or collapse** each parent packet using the **left arrow** in the packet row to view its child packets.
- This mode improves readability by structuring related packets together.

### Ungrouped Packets Mode (Disabled)

![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/UngroupedPackets.png)

- When **Group Packets** is **disabled**, all packets are displayed **individually**.
- The **parent-child relationships are not shown**, and packets appear in a flat list format.
- The **left arrow for expanding packets disappears**, as there are no hierarchical groupings.

This feature helps users customize their view based on preference, offering both a structured, hierarchical display and a flat, simplified list for packet analysis.

## Lock Scroll
![](https://raw.githubusercontent.com/Trefla25/UIDoc/main/LockScroll.png)
If enabled and multiple table grids are present, scrolling on one grid will synchronize the scroll position across all grids to the closest packets (closest packet Id). This feature is only visible with more than one grid.

## Packet Data Grid

Depending on the selected view, the page can feature one or multiple table grids, depending on the selected view, displaying transferred packets within the eHub system. Users have several options for interacting with the data:

- **Sorting:** Users can sort this grid on a specific column.
- **Quick Search:** Easily search for a row by entering a value in the Search field; the grid will display only rows containing the introduced value.
- **Advanced Filtering:** Users can apply advanced filters on columns to filter the displayed data.
- **Select: **Users logged in with administrator rights can select packet rows in order to perform actions (run, delete) on them.

![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/6-GLpNRQjvGfIOT2kBmS0_image.png)

![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/LSsAFJWD7Z52nHtRJTyYi_image.png)

![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/GGjDfbSoqa7WZXYdHlnFJ_image.png)

![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/ro4lrg3wDyY_s1ZLCdebL_image.png)

The data column will display either the full content of the packet or, based on the configured display format, a dialog button, a preview with a dialog button, or a tree view (used for displaying XMLs or JSONs).

Additionally, on the right side of the data column, the status is displayed. The status can be one of the following:
(Talk to Daniel if here should me some more )
- **Processing:**![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/llGJ6WBXxewnfwhBMxtbG_image.png) Indicates that the packet is currently processing.
- **Error:**![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/FV4GzFBfvtWjeUNlcPxtq_image.png) Signifies that the packet encountered an error during processing. In this case, the packet will attempt to retry processing until it succeeds.
- **Fatal Error:**![](https://archbee-image-uploads.s3.amazonaws.com/Ma4eD_toSP-7utQQrz1Gj/IZ_JWiOf-hLpmjoUQSSqs_image.png) Indicates a critical error, and the packet will not attempt further retries. The system proceeds to the next packet. If logged in with administrator rights, the users can manually retry the processing of the packet.

If no status is displayed, it means the packet has successfully completed processing.

# Configuration

Each connector has a default view structure that includes two view tabs: **"ALL"** and **"EACH."**  
- In the **"ALL"** view, a **single data grid** displays all packets.  
- In the **"EACH"** view, **separate data grids** are provided for each distinct channel.

However, to fully utilize the customization features, each Connector Project must create a **'UIViewConfig.json'** file with the following structure:

## UIViewConfig.json

```json
{
    "ViewPacketCount": 5,
    "Views": {
        "View1": {
            "Name": "All",
            "DisplayName": {
                "en": "All",
                "de": "Alle"
            },
            "Channels": [
                {
                    "Name": "D01 -> D02 Data",
                    "DisplayName": {
                        "en": "D01 -> D02 Data",
                        "de": "D01 -> D02 Daten"
                    },
                    "DataDisplay": {
                        "Format": "Dialog"
                    },
                    "Channel": "Device01ToDevice02_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "D02 -> D01 Data",
                    "DisplayName": {
                        "en": "D02 -> D01 Data",
                        "de": "D02 -> D01 Daten"
                    },
                    "Channel": "Device02ToDevice01_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "Errors",
                    "DisplayName": {
                        "en": "Errors",
                        "de": "Errors"
                    },
                    "Channel": "Device01ToDevice02_Data:Error",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "Ack",
                    "DisplayName": {
                        "en": "Ack",
                        "de": "Ack"
                    },
                    "Channel": "Device01ToDevice02_Ack",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                }
            ]
        },
        "View2": {
            "Name": "Each",
            "DisplayName": {
                "en": "Each",
                "de": "jede"
            },
            "Channels": [
                {
                    "Name": "D01 -> D02 Data",
                    "DisplayName": {
                        "en": "D01 -> D02 Data",
                        "de": "D01 -> D02 Daten"
                    },
                    "DataDisplay": {
                        "Format": "Dialog"
                    },
                    "Channel": "Device01ToDevice02_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "D02 -> D01 Data",
                    "DisplayName": {
                        "en": "D02 -> D01 Data",
                        "de": "D02 -> D01 Daten"
                    },
                    "Channel": "Device02ToDevice01_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 2
                    }
                },
                {
                    "Name": "Errors",
                    "DisplayName": {
                        "en": "Errors",
                        "de": "Errors"
                    },
                    "Channel": "Device01ToDevice02_Data:Error",
                    "Position": {
                        "RowIndex": 2,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "Ack",
                    "DisplayName": {
                        "en": "Ack",
                        "de": "Ack"
                    },
                    "Channel": "Device01ToDevice02_Ack",
                    "Position": {
                        "RowIndex": 2,
                        "ColIndex": 2
                    }
                }
            ]
        }
    }
}
```

## Explanations

### General Configuration

- **ViewPacketCount**: Defines the number of packets per page while in offline mode and the maximum packets displayed in live mode. In the example above, it's set to 5.

### Views

Within the "Views" section, you have the flexibility to define as many views as needed. Each view is characterized by the following properties:

- **Name**: A mandatory field representing the view's name.
- **DisplayName**: Translations for the displayed view tab label in multiple languages. If a UI language is unspecified, the view tab will use the "Name" property as its label.
- **Connectors**: A list of connectors that will show this particular view tab. If not specified, the view will be visible to all connectors. The names of the connectors are defined in the "connectors.json" file.
- **DataDisplayFormat**: Determines how data is presented in the UI inside the channel data grid cell, particularly useful for large data. Possible values:
  - **SingleLine**: Data displayed in a single line with horizontal scrolling.
  - **MultiLineFull**: Large data displayed over multiple lines.
  - **MultiLineScroll**: Multi-line display with a fixed height requiring scrolling.
  - **Dialog**: Data shown in a pop-up when clicking a button.
  - **XmlFull / XmlScroll / XmlDialog**: XML format displayed fully, with scrolling, or in a pop-up.
  - **JsonFull / JsonScroll / JsonDialog**: JSON format displayed fully, with scrolling, or in a pop-up.
- **DataRowCount**: Specifies the number of visible rows when using a scroll-based display format. Default is 1.

### Channels

Each view consists of a collection of **channels**, which define the data displayed in the UI as separate grids. Each channel configuration includes:

- **Name**: A mandatory identifier for the channel.
- **DisplayName**: Translations for the displayed data grid title in multiple languages. If omitted, the "Name" property is used.
- **Channel**: The source of the packets displayed in this data grid.
- **DataDisplayFormat**: Overrides the data format for this specific data grid. Can be omitted to inherit from the parent view.
- **DataRowCount**: Overrides the row count set at the view level.
- **Position**: Determines the placement of the channel in the UI. Uses:
  - **RowIndex**: Defines the vertical position (1 for the first row, 2 for the second, etc.).
  - **ColIndex**: Defines the horizontal position (1 for the first column, 2 for the second, etc.).

### Example of View Layout

By modifying the **Position** for each channel, multiple grids can be displayed simultaneously. Each channel requires the **Position** parameter where the user can specify the Row and Column index of the grid.
```json
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
```

#### Default Configuration (All Channels in One Grid)

```json
"Channels": [
                {
                    "Name": "D01 -> D02 Data",
                    "DisplayName": {
                        "en": "D01 -> D02 Data",
                        "de": "D01 -> D02 Daten"
                    },
                    "DataDisplay": {
                        "Format": "Dialog"
                    },
                    "Channel": "Device01ToDevice02_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "D02 -> D01 Data",
                    "DisplayName": {
                        "en": "D02 -> D01 Data",
                        "de": "D02 -> D01 Daten"
                    },
                    "Channel": "Device02ToDevice01_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "Errors",
                    "DisplayName": {
                        "en": "Errors",
                        "de": "Errors"
                    },
                    "Channel": "Device01ToDevice02_Data:Error",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "Ack",
                    "DisplayName": {
                        "en": "Ack",
                        "de": "Ack"
                    },
                    "Channel": "Device01ToDevice02_Ack",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                }
            ]
```

#### Configuration for Separate Grids

```json
"Channels": [
                {
                    "Name": "D01 -> D02 Data",
                    "DisplayName": {
                        "en": "D01 -> D02 Data",
                        "de": "D01 -> D02 Daten"
                    },
                    "DataDisplay": {
                        "Format": "Dialog"
                    },
                    "Channel": "Device01ToDevice02_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "D02 -> D01 Data",
                    "DisplayName": {
                        "en": "D02 -> D01 Data",
                        "de": "D02 -> D01 Daten"
                    },
                    "Channel": "Device02ToDevice01_Data",
                    "Position": {
                        "RowIndex": 1,
                        "ColIndex": 2
                    }
                },
                {
                    "Name": "Errors",
                    "DisplayName": {
                        "en": "Errors",
                        "de": "Errors"
                    },
                    "Channel": "Device01ToDevice02_Data:Error",
                    "Position": {
                        "RowIndex": 2,
                        "ColIndex": 1
                    }
                },
                {
                    "Name": "Ack",
                    "DisplayName": {
                        "en": "Ack",
                        "de": "Ack"
                    },
                    "Channel": "Device01ToDevice02_Ack",
                    "Position": {
                        "RowIndex": 2,
                        "ColIndex": 2
                    }
                }
            ]
```

This setup allows for a structured, organized display where different data categories can be displayed in separate sections rather than being merged into a single data grid.



