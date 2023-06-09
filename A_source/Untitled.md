---
HELPER-CODE-VERSION: v1.0.0-video-note-taking
tag: [youtbube-source]
---


# -

## : Reference
* † https://www.youtube.com/watch?v=C8QOjNSD0a8&ab_channel=BrandonSanderson

## --

## : Transcript Control
* Transcripter will not work if you do not include a youtube.com reference next to the [[#Reference|†]]

```dataviewjs
let $buttonRef = null;
const links = dv.current().file.lists.values;
console.log({links})

const prefix = 'https://www.youtube.com';
const url = findUrl(links, prefix)
function findUrl(links, sep) {
    const found = links?.findLast((link) => {
        return link?.text?.contains(sep)
    })
    return found?.text?.split(sep)[1];
}


const {plugins} = this.app.plugins
const {createButton} = plugins["buttons"]
const yt = plugins['ytranscript'];

const makeOpenBtn = (container, url, name) => createButton({ 
    app, 
    el: container, 
    args: { 
        name,
    },
    clickOverride: {
        click: openView.bind(this),
        params: [{ 
            url, 
            getYtTabEl: getYtTabEl.bind(this),
            yt 
        }],
    },
}) 

makeOpenBtn(this.container, '', 'Refresh')

if (url?.length) {
    console.log({url})
    ubermain(
        main.bind(this), prefix + url)
}



function ubermain(main, url) {
    console.log({url})
    main(url);
}

function main(url) {
    this.container.style = 'border: 3px solid lightblue;margin: .5em 0;'
    const row1 = [
        'YTranscript',
        '。。。。',
        makeOpenBtn(this.container,url, 'Open')
    ];
    $buttonRef = row1[2]
    dv.table(
        '',
        [
            row1,
        ],
    )

    

}
function openView({url, yt, getYtTabEl}) {

    const ytTab = getYtTabEl()
    console.log(this.container, 'button')
    if (ytTab?.tabHeaderCloseEl) {
        ytTab.tabHeaderCloseEl.click()
        $buttonRef.innerText = 'Open';
console.log($buttonRef.previousSibling);
    } else {
        $buttonRef.innerText = 'Close';
        yt.openView(url)
    }
}  
function getYtTabEl() {
    return this.app.workspace.rightSplit
        .children[0]
        ?.children
        .find(findViewPredicate)   
}
function findViewPredicate({tabHeaderEl}) {
    return tabHeaderEl
            ?.dataset?.type 
                === 'transcript-view'
}

```

## :  Timestamp Control Button

*Timestamp Button is required for proper operation.*

* Click button below to open video:
        ```timestamp-url
        ```
    * ⤴ Requires unindent and a url input within codeblock

* Hotkeys:
	* [[timestamp-hotkeys-dataview#--|Control video player without leaving the note]]
	* [[code-block-from-selection-hotkeys#--| Make buttons from url]] 

---

#### ---- Transient Sandbox

### Collection Phase


### Cluster Phase