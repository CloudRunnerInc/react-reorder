# React Reorder

**Drag & drop, touch enabled, reorder / sortable list, React component**

[![CircleCI](https://circleci.com/gh/JakeSidSmith/react-reorder.svg?style=svg)](https://circleci.com/gh/JakeSidSmith/react-reorder)

If you are using v2, please refer to [this documentation](https://github.com/JakeSidSmith/react-reorder/blob/609de5a6be9ae7ea4b032b0b260b08bc524b362e/README.md).

## About

React Reorder is a React component that allows the user to drag-and-drop items in a list (horizontal / vertical), or a grid. You can also allow dragging items from one list to another.

It fully supports touch devices and auto-scrolls when a component is being dragged (check out the [demo](https://jakesidsmith.github.io/react-reorder/)).

It also allows the user to set a hold time (duration before drag begins) allowing additional events like clicking / tapping to be applied.

## Installation

- Using npm

  ```shell
  npm install react-reorder
  ```

  Add `--save` or `-S` to update your package.json

- Using bower
  ```shell
  bower install react-reorder
  ```
  Add `--save` or `-S` to update your bower.json

## Example

1. If using requirejs: add `react-reorder` to your `require.config`

   ```javascript
   paths:
     // <name> : <path/to/module>
     'react-reorder': 'react-reorder/reorder'
   }
   ```

2. If using a module loader (requirejs / browserfiy / commonjs): require `react-reorder` where it will be used in your project

   ```javascript
   var Reorder = require('react-reorder');
   ```

   If using requirejs you'll probably want to wrap your module e.g.

   ```javascript
   define(function(require) {
     // Require react-reorder here
   });
   ```

3. Configuration

   **Note: If your array is an array of primitives (e.g. strings) then `itemKey` is not required as the string itself will be used as the key, however item keys must be unique in any case**

   1. Using JSX

      ```javascript
      <Reorder
        // The key of each object in your list to use as the element key
        itemKey="name"
        // Lock horizontal to have a vertical list
        lock="horizontal"
        // The milliseconds to hold an item for before dragging begins
        holdTime="500"
        // The list to display
        list={[{ name: 'Item 1' }, { name: 'Item 2' }, { name: 'Item 3' }]}
        // A template to display for each list item
        template={ListItem}
        // Function that is called once a reorder has been performed
        callback={this.callback}
        // Class to be applied to the outer list element
        listClass="my-list"
        // Class to be applied to each list item's wrapper element
        itemClass="list-item"
        // A function to be called if a list item is clicked (before hold time is up)
        itemClicked={this.itemClicked}
        // The item to be selected (adds 'selected' class)
        selected={this.state.selected}
        // The key to compare from the selected item object with each item object
        selectedKey="uuid"
        // Allows reordering to be disabled
        disableReorder={false}
      />
      ```

   2. Using standard Javascript

      ```javascript
      React.createElement(Reorder, {
        // The key of each object in your list to use as the element key
        itemKey: 'name',
        // Lock horizontal to have a vertical list
        lock: 'horizontal',
        // The milliseconds to hold an item for before dragging begins
        holdTime: '500',
        // The list to display
        list: [{ name: 'Item 1' }, { name: 'Item 2' }, { name: 'Item 3' }],
        // A template to display for each list item
        template: ListItem,
        // Function that is called once a reorder has been performed
        callback: this.callback,
        // Class to be applied to the outer list element
        listClass: 'my-list',
        // Class to be applied to each list item's wrapper element
        itemClass: 'list-item',
        // A function to be called if a list item is clicked (before hold time is up)
        itemClicked: this.itemClicked,
        // The item to be selected (adds 'selected' class)
        selected: this.state.selected,
        // The key to compare from the selected item object with each item object
        selectedKey: 'uuid',
        // Allows reordering to be disabled
        disableReorder: false,
      });
      ```

4. Callback functions

   1. The `callback` function that is called once a reorder has been performed

      ```javascript
      function callback(
        event,
        itemThatHasBeenMoved,
        itemsPreviousIndex,
        itemsNewIndex,
        reorderedArray
      ) {
        // ...
      }
      ```

   2. The `itemClicked` function that is called when an item is clicked before any dragging begins

      ```javascript
      function itemClicked(event, itemThatHasBeenClicked, itemsIndex) {
        // ...
      }
      ```

      **Note: `event` will be the synthetic React event for either `mouseup` or `touchend`, and both contain `clientX` & `clientY` values (for ease of use)**

## Compatibility / Requirements

Using bower

Add `--save` or `-S` to update your bower.json

```
bower install react-reorder
```

## Example

If using a module loader (requirejs / browserfiy / commonjs): require `react-reorder` where it will be used in your project

```javascript
var Reorder = require('react-reorder');
var reorder = Reorder.reorder;
var reorderImmutable = Reorder.reorderImmutable;
var reorderFromTo = Reorder.reorderFromTo;
var reorderFromToImmutable = Reorder.reorderFromToImmutable;

// Or ES6

import Reorder, {
  reorder,
  reorderImmutable,
  reorderFromTo,
  reorderFromToImmutable,
} from 'react-reorder';
```

### Configuration

```javascript
<Reorder
  reorderId="my-list" // Unique ID that is used internally to track this list (required)
  reorderGroup="reorder-group" // A group ID that allows items to be dragged between lists of the same group (optional)
  getRef={this.storeRef.bind(this)} // Function that is passed a reference to the root node when mounted (optional)
  component="ul" // Tag name or Component to be used for the wrapping element (optional), defaults to 'div'
  placeholderClassName="placeholder" // Class name to be applied to placeholder elements (optional), defaults to 'placeholder'
  draggedClassName="dragged" // Class name to be applied to dragged elements (optional), defaults to 'dragged'
  lock="horizontal" // Lock the dragging direction (optional): vertical, horizontal (do not use with groups)
  holdTime={500} // Default hold time before dragging begins (mouse & touch) (optional), defaults to 0
  touchHoldTime={500} // Hold time before dragging begins on touch devices (optional), defaults to holdTime
  mouseHoldTime={200} // Hold time before dragging begins with mouse (optional), defaults to holdTime
  onReorder={this.onReorder.bind(this)} // Callback when an item is dropped (you will need this to update your state)
  autoScroll={true} // Enable auto-scrolling when the pointer is close to the edge of the Reorder component (optional), defaults to true
  disabled={false} // Disable reordering (optional), defaults to false
  disableContextMenus={true} // Disable context menus when holding on touch devices (optional), defaults to true
  placeholder={
    <div className="custom-placeholder" /> // Custom placeholder element (optional), defaults to clone of dragged element
  }
>
  {this.state.list.map(item => <li key={item.name}>{item.name}</li>).toArray()
  /*
    Note this example is an ImmutableJS List so we must convert it to an array.
    I've left this up to you to covert to an array, as react-reorder updates a lot,
    and if I called this internally it could get rather slow,
    whereas you have greater control over your component updates.
    */
  }
</Reorder>
```

### Callback functions

The `onReorder` function that is called once a reorder has been performed.

You can use our helper functions for reordering your arrays.

```javascript
import { reorder, reorderImmutable, reorderFromTo, reorderFromToImmutable } from 'react-reorder';

onReorder (event, previousIndex, nextIndex, fromId, toId) {
  this.setState({
    myList: reorder(this.state.myList, fromIndex, toIndex);
  });
}

onReorderGroup (event, previousIndex, nextIndex, fromId, toId) {
  if (fromId === toId) {
    const list = reorderImmutable(this.state[fromId], previousIndex, nextIndex);

    this.setState({
      [fromId]: list
    });
  } else {
    const lists = reorderFromToImmutable({
      from: this.state[fromId],
      to: this.state[toId]
    }, previousIndex, nextIndex);

    this.setState({
      [fromId]: lists.from,
      [toId]: lists.to
    });
  }
}
```

## Compatibility / Requirements

- Version `3.x` tested and working with React `15`, but should be backward compatible at least a couple of versions.
