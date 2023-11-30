# ChatGPT_API
!pip install --upgrade openai==0.28.1

import openai
openai.api_key= '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'

!pip install panel

def collect_messages(_):
    prompt = inp.value_input
    inp.value = ''
    context.append({'role':'user', 'content':f"{prompt}"})
    response = get_completion_from_messages(context)
    context.append({'role':'assistant', 'content':f"{response}"})
    panels.append(
        pn.Row('User:', pn.pane.Markdown(prompt, width=600)))
    panels.append(
        pn.Row('Assistant:', pn.pane.Markdown(response, width=600, styles={'background-color': '#F6F6F6'})))

    return pn.Column(*panels)

    import panel as pn  # GUI
pn.extension()

panels = [] # collect display

context = [ {'role':'system', 'content':"""
Your task is to help a recommender to write a LOR for his employer. \
you will complete the task by following these steps sequentially \
first ask the user how would you describe the candidate’s proficiency in SQA-related works (Requirement Understanding, RTM creation, Test Plan making, Test Case Writing, Test Case Execution, Bug Finding, and reporting) and relevant technical skills? \
then ask the user how would you describe the candidate’s proficiency in programming languages (Selenium, Java, Automation)and relevant technical skills? \
then ask the user can you provide examples of the candidate’s problem-solving abilities in challenging technical situations? \
then ask the user what projects or research has the candidate been involved in, and what impact have they had? \
then ask the user how does the candidate approach collaboration and communication within a team or academic setting? \
then ask the user in what ways has the candidate demonstrated their commitment to continuous learning and staying updated on industry trends? \
then ask the user how would you assess the candidate’s analytical and critical thinking skills? \
then ask the user can you highlight any instances where the candidate showed leadership or took initiative in a CS-related context? \
then ask the user what is your opinion on the candidate’s ability to adapt to new technologies and methodologies? \
then ask the user how does the candidate handle pressure or tight deadlines in a computer science environment? \
then ask the user in your view, what sets this candidate apart from others pursuing graduate studies in Computer Science? \



"""} ]


inp = pn.widgets.TextInput(value="Hi", placeholder='Enter text here…')
button_conversation = pn.widgets.Button(name="Chat!")

interactive_conversation = pn.bind(collect_messages, button_conversation)

dashboard = pn.Column(
    inp,
    pn.Row(button_conversation),
    pn.panel(interactive_conversation, loading_indicator=True, height=800),
)
dashboard
