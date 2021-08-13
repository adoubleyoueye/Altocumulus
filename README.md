<h1 align="center">Altocumulus :cloud:</h1>

### :dart: About ###
A tool for generating “word clouds” from text. The clouds give greater prominence to words that appear more frequently in the source text.

> Word clouds are a popular way to visualise large amounts of text. Word clouds are images showing scattered words in different sizes, where words that appear more frequently in the given text are larger, and less common words are smaller or not shown at all

![wordcloud](https://muralweaver.netlify.com/static/e82592d14dff24be2af115fe1db56577/7cc4b/wordcloud.png)

#### The Flow of Interactions 
1. User clicks *Lunch Order* shortcut.
![](./assets/command.png)
3. Event listener sends modal view as [json](./assets/lunch_order_view/json) 

```python 
@app.shortcut("create_order")
def open_modal(ack, shortcut, client):
    # Acknowledge the shortcut request
    ack()
    # Call the views_open method using the built-in WebClient
    client.views_open(
        trigger_id=shortcut["trigger_id"],
        # A simple view payload for a modal
        # view=SLACK_ORDER_BLOCK
        view={go to assets folder to see}
```
3. Shortcut triggers a modal as shown [here](#top).
4. User inputs the item, price and restuarant [or a SQL statement :wink:] then hits submit which sends a POST request to our app. 
5. Payload sent back to the server as json
6. The body of that request will contain a interaction payload parameter, 'view_submission' which contains the values we need. The app parses this payload parameter as JSON.
```@app.view("")
def handle_view_events(ack, body, logger):
    ack()
    response_data = body
    team_id = response_data['user']['team_id']
    user_id = response_data['user']['id']
    form_values = response_data['view']['state']['values']
    modal_values = []
    for v in form_values.values():
        modal_values.append(v['plain_text_input-action']['value'])
    # modal_fields = ['item', 'price', 'restaurant']
    # modal_data = zip(modal_fields, modal_values)
    logger.info(modal_data)

    create_order(user_id, team_id,
                 modal_values[0], modal_values[1], modal_values[2])
```  
7. 

## :japanese_castle: Architectural Decisions ##

- ### Context

- ### Facing

- ### Decided on

- ### and Neglected

- ### to Achieve

- ### ...
## :triangular_ruler: Technologies ##

- Django
- Slack w/ Bolt
- 
## :checkered_flag: Starting ##

```bash
# Clone this project
$ git clone repo

# TBC
...

# The server will initialize on ...
```

## Tests ##

-

## Deployment checklist ##
- `Run manage.py check --deploy`


## :busstop: Roadmap ##

## :blue_book: References
