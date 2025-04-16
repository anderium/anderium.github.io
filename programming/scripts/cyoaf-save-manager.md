<!-- markdownlint-configure-file { "no-inline-html": { "allowed_elements": ["script", "input", "label", "p", "textarea"] } } -->
# CYOAF Save Manager Injector

Adds four scenes and five tags to a CYOA Factory Story to create a save system.

<script>
window.addEventListener('DOMContentLoaded', () => {
  const inputElement = document.getElementById("story")
  const arraysElements = document.getElementById("array-tags")

  const errorElement = document.getElementById("error")
  const outputElement = document.getElementById("output")

  const ADDED_SCENES = [
        {
            "story": "gLhXj-kvvQcLuq7b8U4l4",
            "directions": [
                {
                    "id": 2,
                    "type": "empty",
                    "effects": [
                        {
                            "tag": "ta4i8p-wA",
                            "op": "<t>",
                            "value": "saves == 0",
                            "id": "WW8ysqzuq"
                        },
                        {
                            "tag": "ta4i8p-wA",
                            "op": "<f>",
                            "value": "[]",
                            "id": "DuvXaEQdr"
                        }
                    ],
                    "content": "Set up save storage the first time."
                },
                {
                    "id": 1,
                    "type": "text",
                    "content": "You've entered the save menu! \n\nYou currently have {{ saves | length }} stored saves!\n\n{#- selected_save temporarily stores how many saves there are to show the correct choices. -#}",
                    "effects": [
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "length saves",
                            "id": "rPSVOyLV8"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 4,
                    "type": "choice",
                    "scene": "c2LTlfuxIrx83cTbeKAMK",
                    "label": "Create new save file.",
                    "layout": "top"
                },
                {
                    "id": 7,
                    "type": "choice",
                    "scene": "",
                    "label": "Select “{{ saves[selected_save - 1][0][2] }}”.",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "length saves >= 1",
                            "id": "wHGwDlzYf"
                        },
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "length saves - 1",
                            "id": "dK_Q0r46K"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 8,
                    "type": "choice",
                    "scene": "",
                    "label": "Select “{{ saves[selected_save - 2][0][2] }}”.",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "length saves >= 2",
                            "id": "wHGwDlzYf"
                        },
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "length saves - 2",
                            "id": "dK_Q0r46K"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 9,
                    "type": "choice",
                    "scene": "",
                    "label": "Select “{{ saves[selected_save - 3][0][2] }}”.\n{#- You can add more of these, increment the 3 above, and those in the requirements and effects. -#}",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "length saves >= 3",
                            "id": "wHGwDlzYf"
                        },
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "length saves - 3",
                            "id": "dK_Q0r46K"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 6,
                    "type": "choice",
                    "scene": "",
                    "label": "Select older saves.",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "length saves >= 4",
                            "id": "fIz5tkG2G"
                        },
                        {
                            "tag": "RwARiM7Xa",
                            "op": ":",
                            "value": "-1",
                            "id": "0wN14Jrdu"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 3,
                    "type": "choice",
                    "scene": "",
                    "array": "ndqWDHFfo",
                    "label": "{#- Invisible. Added for future versions. (But this choice is why the above aren't linked; it uses the redirect below.) -#}\n\nSelect “{{ $item[0][2] }}”\n\nTodo? Use blueprints with new references for each save. Doesn't work because you cannot create new instances to reference.",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "false",
                            "id": "djuuNhmSQ"
                        },
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "$item[0][1]",
                            "id": "tttd3HEvs"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 5,
                    "type": "redirect",
                    "scene": "pTokaBACUYkqrfQUkLQLp",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "0 <= selected_save and selected_save < length saves",
                            "id": "BFLj8RSsm"
                        }
                    ]
                },
                {
                    "id": 15,
                    "type": "text",
                    "state": "default",
                    "content": "This is the entire list of saves. Please enter the number corresponding to the save you wish to select. Enter -1 or any other invalid number to exit.\n\n{% for item in saves %}\n{{ item[0][1] }}: {{ item[0][2] }}\n{% endfor %}",
                    "layout": "top"
                },
                {
                    "id": 11,
                    "type": "input",
                    "label": "",
                    "content": "RwARiM7Xa"
                },
                {
                    "id": 12,
                    "type": "redirect",
                    "scene": "pTokaBACUYkqrfQUkLQLp",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "0 <= selected_save and selected_save < length saves",
                            "id": "tFLAgAUAS"
                        }
                    ]
                },
                {
                    "id": 13,
                    "type": "text",
                    "state": "default",
                    "content": "Not a save, re-entering menu.",
                    "layout": "top"
                },
                {
                    "id": 14,
                    "type": "redirect",
                    "scene": "enonyik75EvN5iBbda9NY"
                }
            ],
            "id": "enonyik75EvN5iBbda9NY",
            "title": "Save file manager: Menu",
            "start": true,
            "microcosm": false,
            "act": false,
            "color": null,
            "updated": "2025-04-15T17:03:52.501Z",
            "wc": 179,
            "uid": "a5d686",
            "_meta": {
                "byte_size": 1846,
                "owner_id": "a5d686",
                "updated": "2025-04-11T04:57:04.510000+00:00",
                "level": null,
                "id": "enonyik75EvN5iBbda9NY"
            },
        },
        {
            "story": "gLhXj-kvvQcLuq7b8U4l4",
            "directions": [
                {
                    "id": 1,
                    "type": "text",
                    "content": "Give a name for the new save!",
                    "layout": "top",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "=",
                            "value": "0",
                            "id": "kraSoCRAZ"
                        }
                    ]
                },
                {
                    "id": 2,
                    "type": "input",
                    "content": "Q76jxDI6X",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "=",
                            "value": "0",
                            "id": "-z8xYQsU6"
                        }
                    ]
                },
                {
                    "id": 3,
                    "type": "text",
                    "state": "default",
                    "content": "Saving to “{{ new_save_name }}”...",
                    "auto_advance": true,
                    "layout": "top",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "=",
                            "value": "0",
                            "id": "CHGkxIun_"
                        }
                    ]
                },
                {
                    "id": 15,
                    "type": "text",
                    "state": "default",
                    "auto_advance": true,
                    "content": "Running dev test: Creating fake save of incrementing integers and asserting that loading and saving a second time gives the same result. If you have complicated saves, this test might incorrectly fail, use your best judgement for its results.",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "new_save_name == \"developer test\"",
                            "id": "98osfShKZ"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 9,
                    "type": "layout",
                    "persistence": "manual",
                    "effects": [
                        {
                            "tag": "Q76jxDI6X",
                            "op": "<t>",
                            "value": "new_save_name == \"developer test\"",
                            "id": "AJENBMszF"
                        },
                        {
                            "tag": "3g4ixJYLF",
                            "op": ":",
                            "value": "1",
                            "id": "rnX52zoGr"
                        }
                    ]
                },
                {
                    "id": 4,
                    "type": "empty",
                    "effects": [
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "[[\"save_version_1\", length saves, new_save_name], \n\nwhat,\nto,\nsave\n]",
                            "id": "WVVxdGBF6"
                        },
                        {
                            "tag": "ta4i8p-wA",
                            "op": "<f>",
                            "value": "saves || [selected_save]",
                            "id": "IfWGCLzn_"
                        }
                    ],
                    "content": "YOU MUST CHANGE THE FORMULA FOR THE FIRST TAG {selected_save}!\n\nIn it, replace 'what, to, save' with the tags that need to be saved. If you've published your game and add things, change the \"save_version_1\" to different text. Keep it between quotes (\").\n\nTo test it, create a save called \"developer test\" without the quotes."
                },
                {
                    "id": 5,
                    "type": "text",
                    "state": "default",
                    "content": "Done!",
                    "layout": "top",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "=",
                            "value": "0",
                            "id": "dg0CNuJ-Q"
                        }
                    ]
                },
                {
                    "id": 6,
                    "type": "redirect",
                    "scene": "enonyik75EvN5iBbda9NY",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "=",
                            "value": "0",
                            "id": "r6prXu6n4"
                        }
                    ]
                },
                {
                    "id": 7,
                    "type": "redirect",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "=",
                            "value": "1",
                            "id": "2lWc2k6sQ"
                        },
                        {
                            "tag": "ta4i8p-wA",
                            "op": "<f>",
                            "value": "created_save = saves[length saves - 1];\nactual_saves_shouldnt_disappear = slice(saves, 0, length saves - 1);\nfake_save = map(increment(x, idx) = idx ? \"\" || idx : x, created_save);\nactual_saves_shouldnt_disappear || [fake_save]\n",
                            "id": "9ZVN0Ld9A"
                        },
                        {
                            "tag": "Q76jxDI6X",
                            "op": ":",
                            "value": "developer test result",
                            "id": "A8NPIxUVo"
                        },
                        {
                            "tag": "3g4ixJYLF",
                            "op": ":",
                            "value": "1",
                            "id": "z_KTbOpDu"
                        },
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "length saves - 1",
                            "id": "gg11E5TyC"
                        }
                    ],
                    "scene": "wQDfneExTrbgA9VfYjrCS"
                },
                {
                    "id": 8,
                    "type": "text",
                    "state": "default",
                    "content": "Comparing results...",
                    "auto_advance": true,
                    "layout": "top"
                },
                {
                    "id": 14,
                    "type": "empty",
                    "content": "Compares these:\n\"developer test\"\n\"developer test result\"\n\nStores mismatches in save_dev_test, and sets it to 0 if it's successful.",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "<f>",
                            "value": "fake_save = saves[length saves - 2];\nresave = saves[length saves - 1];\nmismatches = [];\nmap(is_equal(x, idx) = x == resave[idx] or idx == 0 ? 0 : subset(mismatches, length mismatches, [x, resave[idx]]), fake_save);\nlength mismatches ? mismatches: 0",
                            "id": "bA_XE6qVv"
                        }
                    ]
                },
                {
                    "id": 13,
                    "type": "text",
                    "state": "default",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "<t>",
                            "value": "save_dev_test == 0",
                            "id": "-Bk_p6H6o"
                        }
                    ],
                    "content": "Everything seems okay!",
                    "layout": "top"
                },
                {
                    "id": 12,
                    "type": "text",
                    "state": "default",
                    "content": "There are mismatches! X → Y means that where a value of X was expected, a value of Y was found. Check those positions! (Y=0 means it isn't set properly, other values mean you swapped tags around.)\n\n{% for mismatch in save_dev_test %}\n{{mismatch[0]}} → {{mismatch[1]}}\n{% endfor %}",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "#",
                            "value": null,
                            "id": "1CZ8mydJu"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 10,
                    "type": "clear"
                },
                {
                    "id": 11,
                    "type": "redirect",
                    "scene": "enonyik75EvN5iBbda9NY",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "x",
                            "value": null,
                            "id": "jBAsDKv8X"
                        },
                        {
                            "tag": "ta4i8p-wA",
                            "op": "<f>",
                            "value": "slice(saves, 0, length saves - 2);",
                            "id": "Qet7wJ0Lf"
                        }
                    ]
                }
            ],
            "id": "c2LTlfuxIrx83cTbeKAMK",
            "title": "!! Save file manager: New save",
            "start": false,
            "microcosm": false,
            "act": false,
            "color": null,
            "wc": 189,
            "uid": "a5d686",
            "_meta": {
                "byte_size": 2186,
                "owner_id": "a5d686",
                "updated": "2025-04-11T14:27:07.918000+00:00",
                "level": null,
                "id": "c2LTlfuxIrx83cTbeKAMK"
            },
            "updated": "2025-04-15T17:07:49.639Z",
        },
        {
            "story": "gLhXj-kvvQcLuq7b8U4l4",
            "directions": [
                {
                    "id": 1,
                    "type": "text",
                    "content": "You've selected “{{ saves[selected_save][0][2] }}”",
                    "layout": "top"
                },
                {
                    "id": 2,
                    "type": "choice",
                    "scene": "wQDfneExTrbgA9VfYjrCS",
                    "label": "Load save",
                    "layout": "top"
                },
                {
                    "id": 3,
                    "type": "choice",
                    "scene": "",
                    "label": "Rename save",
                    "effects": [
                        {
                            "tag": "Q76jxDI6X",
                            "op": "x",
                            "value": null,
                            "id": "AeME1zyLC"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 4,
                    "type": "choice",
                    "scene": "enonyik75EvN5iBbda9NY",
                    "label": "Delete save",
                    "thoughts": [
                        "Are you sure?",
                        "Alright, next click will delete it."
                    ],
                    "effects": [
                        {
                            "tag": "ta4i8p-wA",
                            "op": "<f>",
                            "value": "before = slice(saves, 0, selected_save);\nafter = slice(saves, selected_save + 1, length saves + 1);\nmap(decrement_index(x) = subset(x[0], 1, x[0][1] - 1), after);\nbefore || after",
                            "id": "mfIIj9yNw"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 5,
                    "type": "input",
                    "content": "Q76jxDI6X",
                    "effects": []
                },
                {
                    "id": 6,
                    "type": "empty",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<t>",
                            "value": "subset(saves[selected_save][0], 2, new_save_name)",
                            "id": "CEjxPGKFB"
                        }
                    ],
                    "content": "This uses the side-effect of the `subset` function to do the tag modification without changing any of the array pointers."
                },
                {
                    "id": 7,
                    "type": "redirect",
                    "scene": "enonyik75EvN5iBbda9NY"
                }
            ],
            "id": "pTokaBACUYkqrfQUkLQLp",
            "title": "Save file manager: Selected save",
            "start": false,
            "microcosm": false,
            "act": false,
            "color": null,
            "wc": 48,
            "uid": "a5d686",
            "_meta": {
                "byte_size": 1670,
                "owner_id": "a5d686",
                "updated": "2025-04-11T14:27:13.003000+00:00",
                "level": null,
                "id": "pTokaBACUYkqrfQUkLQLp"
            },
            "updated": "2025-04-15T16:53:15.043Z",
        },
        {
            "story": "gLhXj-kvvQcLuq7b8U4l4",
            "directions": [
                {
                    "id": 1,
                    "type": "text",
                    "content": "Loading “{{ selected_save[0][2] }}”...",
                    "auto_advance": true,
                    "effects": [
                        {
                            "tag": "RwARiM7Xa",
                            "op": "<f>",
                            "value": "saves[selected_save]",
                            "id": "KOqX7oBjI"
                        }
                    ],
                    "layout": "top"
                },
                {
                    "id": 2,
                    "type": "empty",
                    "content": "This is the opposite of the save function. Set back all the tags by using the order you defined before. Start counting at 1.",
                    "effects": [
                        {
                            "tag": null,
                            "op": "<f>",
                            "value": "selected_save[1]",
                            "id": "aY4MN_M6B"
                        },
                        {
                            "tag": null,
                            "op": "<f>",
                            "value": "selected_save[2]",
                            "id": "fdVJhtqIG"
                        },
                        {
                            "tag": null,
                            "op": "<f>",
                            "value": "selected_save[3]",
                            "id": "zYqnrVg-A9"
                        }
                    ]
                },
                {
                    "id": 4,
                    "type": "notes",
                    "content": "You probably want to do a check to send the reader to the correct place with a redirect.\n\nRemember to set back your custom layout settings if you're not using the default!",
                    "tasks": [
                        {
                            "id": 0,
                            "complete": false,
                            "content": "Layout settings"
                        },
                        {
                            "id": 1,
                            "complete": false,
                            "content": "Redirects"
                        }
                    ]
                },
                {
                    "id": 6,
                    "type": "redirect",
                    "scene": "c2LTlfuxIrx83cTbeKAMK",
                    "effects": [
                        {
                            "tag": "3g4ixJYLF",
                            "op": "#",
                            "value": null,
                            "id": "pzKqT14fe"
                        },
                        {
                            "tag": "3g4ixJYLF",
                            "op": ":",
                            "value": "2",
                            "id": "IIXWsuRGb"
                        }
                    ]
                },
                {
                    "id": 5,
                    "type": "layout",
                    "layout": "bottom",
                    "persistence": "block"
                },
                {
                    "id": 3,
                    "type": "redirect"
                }
            ],
            "id": "wQDfneExTrbgA9VfYjrCS",
            "title": "!! Save file manager: Load save",
            "start": false,
            "microcosm": false,
            "act": false,
            "color": null,
            "wc": 75,
            "uid": "a5d686",
            "_meta": {
                "byte_size": 1132,
                "owner_id": "a5d686",
                "updated": "2025-04-11T14:27:16.059000+00:00",
                "level": null,
                "id": "wQDfneExTrbgA9VfYjrCS"
            },
            "updated": "2025-04-15T17:04:57.310Z",
        }
    ]

  const ADDED_TAGS = [
        {
            "name": "new_save_name",
            "id": "Q76jxDI6X",
            "format": "text",
            "type": "tag",
            "default": "",
            "precision": ""
        },
        {
            "name": "saves",
            "id": "ta4i8p-wA",
            "format": "",
            "type": "tag",
            "default": "",
            "precision": "",
            "referencing": "",
            "arrayFill": "Include the following..."
        },
        {
            "name": "saves_choice_generator",
            "id": "ndqWDHFfo",
            "type": "array",
            "default": "",
            "referencing": ""
        },
        {
            "name": "selected_save",
            "id": "RwARiM7Xa",
            "format": "",
            "type": "tag"
        },
        {
            "name": "save_dev_test",
            "id": "3g4ixJYLF",
            "format": "",
            "type": "tag"
        }
    ]

  inputElement.addEventListener("change", handleFiles, false)
  inputElement.disabled = false

  function handleFiles() {
    errorElement.style.display = "none"
    const fileList = this.files;
    if (fileList.length > 1) {
      console.log("Cancelling operation on more than one file.")
      errorElement.innerHTML = "Error: More than one file selected. Please select each story individually."
      errorElement.style.display = "block"
      return
    }
    if (fileList.length <= 0) {
      console.log("Cancelling operation on missing file.")
      errorElement.innerHTML = "Error: No file selected. Please select a story."
      errorElement.style.display = "block"
      return
    }
    const file = fileList[0]
    if (!file.name.endsWith(".json")) {
      console.log("Cancelling operation on non JSON file.")
      errorElement.innerHTML = "Error: Please upload the story JSON, not a zip or other file formats."
      errorElement.style.display = "block"
      return
    }

    handleStoryFile(file)
  }

  /**
   * @param {File} file
  */
  function handleStoryFile(file) {
    errorElement.style.display = "none"
    file.text().then(
      (storyJSON) => {
        handleStory(JSON.parse(storyJSON), file.name)
      },
      (reason) => {
        console.error("Failed to load story.", reason)
        errorElement.innerHTML = "Error: Failed to load story. Please try again."
        errorElement.style.display = "block"
      }
    )
  }

  let ignore_version_problem = false;
  /**
   * @param {Object} story
   * @param {String} filename
   */
  function handleStory(story, filename) {
    errorElement.style.display = "none"
    console.log("Story Object:", story)
    if (story.version !== 3 && !ignore_version_problem) {
      console.warn("Failed to load story.")
      errorElement.innerHTML = "Warning: Story save version is unknown. Try again to ignore."
      errorElement.style.display = "block"
      ignore_version_problem = true;
      return
    }

    const array_names = arraysElements.value.split(",").filter(x=>x).map(x=>x.trim())
    const tags_and_arrays = story.tags.filter(x => x.type === "tag")
    const tags = tags_and_arrays.filter(x => array_names.indexOf(x.name) === -1)
    ADDED_SCENES[1].directions[5].effects[0].value = `[["save_version_1", length saves, new_save_name],

${tags.map(x => x.name).join(',\n')}${tags && array_names ? ',' : ''}
${array_names.map(x => x + " || []").join(',\n')}
]`
    ADDED_SCENES[3].directions[1].effects = tags.map((x, index) => { return {
            "tag": x.id,
            "op": "<f>",
            "value": `selected_save[${1 + index}]`,
            "id": "aY4MN_M6B"
        }}
    )
    ADDED_SCENES[3].directions[1].effects.push(
        ...tags_and_arrays.filter(x => array_names.indexOf(x.name) !== -1)
        .map((x, index) => { return {
                "tag": x.id,
                "op": "<f>",
                "value": `selected_save[${tags.length + 1 + index}] || []`,
                "id": "aY4MN_M6B"
            }}
        )
    )

    story.updated = new Date().getTime()
    story.scenes.push(...ADDED_SCENES)
    story.tags.push(...ADDED_TAGS)
    console.log("Injected save manager into story!")

    if (!story.settings.overlayout) {
      console.warn("Story has overlayout disabled.")
      errorElement.innerHTML = "Warning: You have not enabled overlayout, this might result in visual bugs."
      errorElement.style.display = "block"
    }

    const blob = new Blob([JSON.stringify(story, undefined, 2)], { type: "application/json" });
    outputElement.innerHTML = `<a download="${filename || "story.json"}" href="${window.URL.createObjectURL(blob)}">Download result.</a> <span style="color: red;">New tags must be manually added!</span>`
  }
})
</script>

## Input file

<label for="story">Story file to add save to</label>: <input type="file" id="story" disabled>

<label for="array-tags">Put tags that are arrays here, if any (comma separated)</label>: <textarea id="array-tags"></textarea>

## Output file

<p id="error" style="display: none; color: red;">Error</p>

<p id="output">Output will be here</p>

You should redirect to the save menu in places where readers may make saves. You should add redirects from the “load
save” scene to wherever the readers need to return after loading their save.

To add tags once you've already injected the save manager you need to edit two scenes. They are marked with two
exclamation marks (!!) in front of them. These scenes contain additional instructions. Simply put you need to manually
add the new tags to the formula that creates the save, and manually match them in the save loading.
