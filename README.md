#jQuery winPop

jQuery winPop makes it easy to work with native Browser window popups.

-------------

## Default Settings
     {
          width: 600,
          height: 400,
          
          top: 0,
          left: 0,
          center: true,
          
          title: 'Untitled Document',
          name: 'newWindow',
          
          head: '',
          body: {
            elem: '',
            method: 'html'
          },  
          
          eventName: 'click',
          delegateElem : '',
          
          callBefore: undefined,
          callAfter: undefined
     }


## Example Usage
Load the plugin file after jQuery

    <script type="text/javascript" src="winPop.js"></script>

Prepare some content to append to the head of the new window's document

    var popupHead = '<style>';
    popupHead += 'body { background: #f0f0f0; }';
    popupHead += '</style>';

Call the plugin on an element with the desired settings and you're done

    $('.popup').winPop({
      // Popup document <title>
      title: 'Lorem Ipsum',
      
      // Popup name
      name: 'loremIpsum',
    
      // The stuff you want to put in the <head> of the popup document
      head: popupHead,
    
      // The stuff that goes in the <body>
      body: {
        // Selector to retrieve the body's content from and add it to the newly created window - e.g. { elem: '#main' }
        // If elem is empty or not set, the element that called winPop will be used
        elem: '',
        
        // How should we grab the content. Choose between 'outerhtml', 'html', and 'text'
        method: 'outerhtml'
      },
    
      // Which element should trigger the popup window? If not set, the element that called winPop triggers the popup
      delegateElem: 'a[data-rel="ul-popup"]',
  
      // Do stuff before the popup window opens. Access is given to the options object
      callBefore: function (opts) { 
        // Log the options object
        console.log('options: ', opts); 
        
        // Perhaps you want to change its document title before the new window opens
        opts.title = "New Ipsum"; 
      },

      // The native Browser window is set as a parameter to this callback
      callAfter: function (browserWin) {
        // Since we have access to the window, we also have access to its document
        console.log('browser window: ', browserWin.document);
        
        // Manipulate the new popup's document contents as needed
        $(browserWin.document.body).prepend("<h2>Welcome</h2>");
        
        // or print the popup's document
        //browserWin.print();
  
        /* 
        window.setTimeout(function() {
          // close it programmatically if needed
          browserWin.close();
        }, 2000);
        */
      }
    });

