- **OpenAI API**
	- Each request to the API, we need to pass it a model and an array of messages. We can add in optional settings to.
- A **Large Language Model** is an algorithm that uses training data to recognize patterns and make predictions or decisions.
- gpt-4 (gpt-3.5-turbo) is the model to use for text generation.
- **Array of Messages**
	- More like an array of objects.
	- It would contain a system object for instructions.
	- It would contain a user object for user's input
	- We send these messages to OpenAI and it would return an assistant object that would contain the AI output.
- **Chat Completions API**
	-  Endpoint to use for any text generation projects.
- **Tokens**
	- Your tokens are your context window. Tokens cost credit and they need processing. Keeping tokens low saves time and money.
	- max_tokens setting limits the number of tokens the model outputs, but it does not affect the size of your input (Just change your prompt length for your system)
		- does not allow us to control how concise a text is.
- **Temperature**
	- Controls how daring output is. Can be set from 0-2. Lower temperature is less daring and higher temperature is more daring. Default is 1.
		- Lower is safer, more predictable. Good for factual output
		- Higher is dangerous, less predictable
		- Good for creative output (maybe)
- **Few Shot Approach**
	- Providing the model with one or more examples of text output that we want. Tend to use if we failing to get results with original prompt.
	- Pros:
		- More control over style of output
	- Cons:
		- More expensive (tokens)
		- Less performance
- **Stop Sequence**
	- Reasons a model stops producing:
		- Finished what it wanted to do
		- Ran out of tokens
		- Encountered a stop sequence
	-  It is an array with up to 4 stop sequences. The model stops generating when it tries to produce a stop sequence and the outputted text will not include a stop sequence.
- **Presence and Frequency Penalties**
	- presence_penalty
		- Number from -2 to 2
		- Defaults to 0
		- Higher numbers increases a model's likelihood to talk about new topics.
	- frequence_penalty
		- Number from -2 to 2
		- Defaults to 0
		- Higher numbers decreases a model' likelihood of repeating the exact same phrase.
- **Fine-Tuning**
	- Giving a standard, pre-trained model a specific data set to enhance its performance on a particular task.
	- Last resort
		- Work on prompt-design
		- Adjust settings e.g. temperature
		- Use few-shot approach
		- Then fine-tune
	- At least 50 items (human-checked) and JSONL format
	- Use-cases
		- Tone and style
			- Teach how to respond
		- Format
			- Like JSON data
		- Function calling
		- Financial motivations
			- Reducing few-shot prompt-sizes
			- Downgrading the model
	- ```javascript
	  const openai = newOpenAI(
		  {dangerouslyAllowBrowser:true}
	  )
	  // Upload training data
	  const upload = await openai.files.create({
		  file: await fetch('/motivationalBotData.jsonl'),
		  purpose: 'fine-tune'
	  })
	  // Use file ID to create job from upload
	  const fineTune = await openai.fineTuning.jobs.create({
		  training_file: 'fileID',
		  model: 'gpt-3.5-turbo'
	  })
	  // Check status of job
	  const fineTuneStatus = await openai.fineTuning.jobs.retrieve('jobStatus')
	  // you will get a fine_tuned-model : "fineModel"
	  // put this as your model instead of gpt-4
	  ```
- **OpenAI API Dependency**
	- npm install openai
	- ```javascript
	  import OpenAI from 'openai'
	  const openai = new OpenAI({
		  dangerouslyAllowBrowser: true //remove later
	  })
	  const messages = [
		  {
			  role: 'system',
			  content: 'You are a helpful general knowledge expert. Use examples provided between ### to set the style and tone of your response.'
		  },
		  {
			  role: 'user'.
			  content: 'Who invented the television? ### Mom ###'
		  }
	  ]
	  const response await openai.chat.completions.create({
		  model: 'gpt-4',
		  messages: messages,
		  max_tokens: 16, // Limits tokens, default: infinity
		  temperature: 1.1, // Temperature of the model  
		  stop: ['3.'], // Stop sequence. Ex: Stops to only 2 points in a list
		  presence_penalty: 0, 
		  frequency_penalty: 0
	  });
	  console.log(response.choices[0].message.content)
	  ```
  - **Prompt Engineering**
	  - The art or science of designing inputs for generative AI tools like gpt-4 to produce optimal outputs.
- **Generating Images**
	- ```javascript
	  const response = await openai.images.gerate({
		  model: 'dall-e-3', //default dall-e-2
		  prompt: prompt, //required
		  n: 1, // default 1, 1-10 how many images generated
		  size: '1024x1024', // default 1024x1024
		  style: 'vivid', //default vivid, other option: natural
		  response_format: 'url' //default url, could do b64_json
	  })
	  response.data[0].url
	  data:image/png;base64, response.data[0].b64_json
	  ```
	  - OpenAI image URLs last for one hour. Only useful for a single session.
  - **AI Safety**
	  -  Four types of AI risks
		  - Misuse
			  - Short Term: Deepfakes, fake news, prompt injections
				  - Prompt Injections: a new attack technique that enables attackers to manipulate the output of the LLM.
			  - Long Term: AI-enabled dictatorship
		  - Accidental
			  - Short Term: Self-driving car crash
			  - Long Term: Entire country ran on Ai.. - alignment problem
	  - If you build AI agents with access to general tools, you should expect misuse through prompt injections.
	  - Safety Best Practices
		  - There is a link on OpenAI website
		  - ```javascript
		    const completion = await openai.moderations.create({
			    input: "I hate you",
			    user: 'user_123'
		    })
		    const {flagged, categories} = completion.results[0];
		    // Flagged is true/false, categories is where it fall unders.
		    ```
		- Adversarial Testing - Test your model beforehand
		- End-users IDs when interacting with the model