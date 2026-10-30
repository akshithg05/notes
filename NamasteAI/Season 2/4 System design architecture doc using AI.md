
Things we have done until now

![[namastedev.com_learn_namaste-ai_system-design-architecture-documentation-using-ai.png]]

From here it will be the Engineering standpoint of things. Until now we have done what a Project / Product manager would do things.

Next things of action - PRD looks good, now lets move to creating a System design architecture document.  Preferences - Build a monolith application . Use MERN stack and use NextJS instead of React for UI along with TypeScript. NodeJS for backend. MongoDB hosted on the web for database managed by mongoDB.
IMage storage im thinking we can use google drive. If I use s3, cloudflare r2 I might be charged I guess.
These are my preferences. Ask me questions for clarity and give me suggestions which best suits our application.
(For now I just want us to discuss the architecture not create the document as of now. I want to discuss important questions and ask me questions if required)

(Guide AI to do well, sometimes it can give total garbage and gibberish. We need to be patient and ask questions. Understand whatever AI is doing and ask the decision. DO not fully blindly let it do the work).

Use mongodb atlas

Important decision - database, techstack.
Driver - mongoose (library), it is a JS library used to interact with mongodb using javascript.
also we can use Zod for API requests.

Wedding member invitation flow in the email.
Wedding members need not verify email ID.

Photos should never go into mongoDB. Itsnot meant for it.

Image maybe s3, cloudflare r2. whichever has a free plan,, but I want free services., else I need to use my google drive link only.

Email maybe Resend, because free service, we want to stick to free services.

Maybe vercel for nodejs deployment. (AWS is paid and I want to stick to free services, maybe later migrate it). Or any free providers is enough , aws is not free i suppose. What if i take a cheap instance, will it be free ?

Basic application logs, do not require complex logging systems like cloudwatch or sentry.

Rate limiting.

Multi- tenancy for weddings.

 Guest approvals need not require any approval mechanism.
 
 Analytics may not be required, activity is enough in the workspace.

(Dont create a sys design doc, first consider all points above and give a summary of all decisions, once I approve it, we can create the system design document.)


More time you spend on planning ,lesser time you spend on bugs and defects and changes.
If requirements are clear things will be clear and go ahead smoothly.





