# Shedding light on AI bias with real world examples

## by: [IBM Data and AI Team](https://www.ibm.com/blog/author/ibm-data-and-ai/ "IBM Data and AI Team, Author at IBM Blog")

As companies increase their use of artificial intelligence (AI), people are questioning the extent to which human biases have made their way into AI systems. Examples of AI bias in the real world show us that when discriminatory data and algorithms are baked into AI models, the models deploy biases at scale and amplify the resulting negative effects.

Companies are motivated to tackle the challenge of bias in AI not only to achieve fairness, but also to ensure better results. However, just as systemic racial and gender bias have proven difficult to eliminate in the real world, eliminating bias in AI is no easy task.

In the article, [_What AI can and can’t do (yet) for your business_](https://www.mckinsey.com/capabilities/quantumblack/our-insights/what-ai-can-and-cant-do-yet-for-your-business "What AI can and can’t do (yet) for your business - McKinsey"), authors Michael Chui, James Manyika, and Mehdi Miremadi of McKinsey noted, “Such biases have a tendency to stay embedded because recognizing them, and taking steps to address them, requires a deep mastery of data-science techniques, as well as a more meta-understanding of existing social forces, including data collection. In all, debiasing is proving to be among the most daunting obstacles, and certainly the most socially fraught, to date.”

Examples of AI bias from real life provide organizations with useful insights on how to identify and address bias. By looking critically at these examples, and at successes in overcoming bias, data scientists can begin to build a roadmap for identifying and preventing bias in their machine learning models. 

## What is bias in artificial intelligence?

AI bias, also referred to as machine learning bias or algorithm bias, refers to AI systems that produce biased results that reflect and perpetuate human biases within a society, including historical and current social inequality. [_Bias can be found in_](https://www.ibm.com/opensource/open/projects/ai-fairness-360/ "AI Fairness 360 - Open Source IBM") the initial training data, the algorithm, or the predictions the algorithm produces.

When bias goes unaddressed, it hinders people’s ability to participate in the economy and society. It also reduces AI’s potential. Businesses cannot benefit from systems that produce distorted results and foster mistrust among people of color, women, people with disabilities, the LGBTQ community, or other marginalized groups of people.

## The source of bias in AI

Eliminating AI bias requires drilling down into datasets, machine learning algorithms and other elements of AI systems to identify sources of potential bias.

### Training data bias

AI systems learn to make decisions based on training data, so it is essential to assess datasets for the presence of bias. One method is to review data sampling for over- or underrepresented groups within the training data. For example, training data for a facial recognition algorithm that over-represents white people may create errors when attempting facial recognition for people of color. Similarly, security data that includes information gathered in geographic areas that are predominantly black could create racial bias in AI tools used by police.

Bias can also result from how the training data is labeled. For example, AI recruiting tools that use inconsistent labeling or exclude or over-represent certain characteristics could eliminate qualified job applicants from consideration.

### Algorithmic bias

Using flawed training data can result in algorithms that repeatedly produce errors, unfair outcomes, or even amplify the bias inherent in the flawed data. Algorithmic bias can also be caused by programming errors, such as a developer unfairly weighting factors in algorithm decision-making based on their own conscious or unconscious biases. For example, indicators like income or vocabulary might be used by the algorithm to unintentionally discriminate against people of a certain race or gender.

### Cognitive bias

When people process information and make judgments, we are inevitably influenced by our experiences and our preferences. As a result, people may build these biases into AI systems through the selection of data or how the data is weighted. For example, cognitive bias could lead to favoring datasets gathered from Americans rather than sampling from a range of populations around the globe.

According to NIST, this source of bias is more common than you might think. In its report [_Towards a Standard for Identifying and Managing Bias in Artificial Intelligence (NIST Special Publication 1270)_](https://www.nist.gov/news-events/news/2022/03/theres-more-ai-bias-biased-data-nist-report-highlights "There’s More to AI Bias Than Biased Data, NIST Report Highlights - NIST"), NIST noted that “human and systemic institutional and societal factors are significant sources of AI bias as well, and are currently overlooked. Successfully meeting this challenge will require taking all forms of bias into account. This means expanding our perspective beyond the machine learning pipeline to recognize and investigate how this technology is both created within and impacts our society.”

## Examples of AI bias in real life

As society becomes more aware of how AI works and the possibility for bias, organizations have uncovered numerous high-profile examples of bias in AI in a wide range of use cases.

- **Healthcare**—Underrepresented data of women or minority groups can skew predictive AI algorithms. For example, computer-aided diagnosis (CAD) systems have been found to return lower accuracy results for black patients than white patients.
    
- **Applicant tracking systems**—Issues with natural language processing algorithms can produce biased results within applicant tracking systems. For example, [Amazon](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G "Insight - Amazon scraps secret AI recruiting tool that showed bias against women - Reuters") stopped using a hiring algorithm after finding it favored applicants based on words like “executed” or “captured,” which were more commonly found on men’s resumes.
    
- **Online advertising**—Biases in search engine ad algorithms can reinforce job role gender bias. Independent research at Carnegie Mellon University in Pittsburgh revealed that [Google’s online advertising system](https://www.washingtonpost.com/news/the-intersect/wp/2015/07/06/googles-algorithm-shows-prestigious-job-ads-to-men-but-not-to-women-heres-why-that-should-worry-you/ "Google’s algorithm shows prestigious job ads to men, but not to women. - The Washington Post") displayed high-paying positions to males more often than to women.
    
- **Image generation**—[Academic research](https://theconversation.com/ageism-sexism-classism-and-more-7-examples-of-bias-in-ai-generated-images-208748#:~:text=There%20were%20also%20notable%20differences,of%20more%20fluid%20gender%20expression. "Ageism, sexism, classism and more: 7 examples of bias in AI-generated images") found bias in the generative AI art generation application Midjourney. When asked to create images of people in specialized professions, it showed both younger and older people, but the older people were always men, reinforcing gendered bias of the role of women in the workplace.
    
- **Predictive policing tools**—[AI-powered predictive policing](https://www.technologyreview.com/2021/02/05/1017560/predictive-policing-racist-algorithmic-bias-data-crime-predpol/#:~:text=It%27s%20no%20secret%20that%20predictive,lessen%20bias%20has%20little%20effect. "Predictive policing is still racist—whatever data it uses - MIT Technology Review") tools used by some organizations in the criminal justice system are supposed to identify areas where crime is likely to occur. However, they often rely on historical arrest data, which can reinforce existing patterns of racial profiling and disproportionate targeting of minority communities.
    

## Reducing bias and AI governance

Identifying and addressing bias in AI begins with AI governance, or the ability to direct, manage and monitor the AI activities of an organization. In practice, AI governance creates a set of policies, practices and frameworks to guide the responsible development and use of AI technologies. When done well, AI governance ensures that there is a balance of benefits bestowed upon businesses, customers, employees and society as a whole.

Through AI governance policies, companies can build the following practices:

- Compliance—AI solutions and AI-related decisions must be consistent with relevant industry regulations and legal requirements.
    
- Trust—Companies that work to protect customers’ information build brand trust and are more likely to create trustworthy AI systems.
    
- Transparency—Because of the complexity of AI, an algorithm can be a black box system with little insight into the data used to create it. Transparency helps ensure that unbiased data is used to build the system and that results will be fair.
    
- Efficiency—One of the biggest promises of AI is reducing hands-on work and saving employees time. AI should be designed to help achieve business goals, improve speed to market and reduce costs.
    
- Fairness—AI governance often includes methods that aim to assess fairness, equity and inclusion. Approaches like counterfactual fairness identify bias in a model’s decisions and ensure equitable results even when sensitive attributes, such as gender, race, or sexual orientation, are changed.
    
- Human touch—Processes like the “human-in-the-loop” system offer options or make recommendations that are then reviewed by humans before a decision is made to provide another layer of quality assurance.
    
- Reinforced learning—This unsupervised learning technique uses rewards and punishments to teach a system to learn tasks. [McKinsey notes](https://www.mckinsey.com/capabilities/quantumblack/our-insights/what-ai-can-and-cant-do-yet-for-your-business "What AI can and can’t do (yet) for your business - McKinsey") that reinforcement learning transcends human biases and has the potential to yield “previously unimagined solutions and strategies that even seasoned practitioners might never have considered.”
    

## Bias, AI and IBM

A proper technology mix can be crucial to an effective data and AI governance strategy, with a [modern data architecture](https://www.ibm.com/resources/the-data-differentiator/data-architecture "Build a modern data architecture - IBM") and trustworthy AI platform being key components. Policy orchestration within a data fabric architecture is an excellent tool that can simplify the complex AI audit processes. By incorporating AI audit and related processes into the governance policies of your data architecture, your organization can help gain an understanding of areas that require ongoing inspection.

At [IBM Consulting,](https://www.ibm.com/consulting/talent-management "HR and Talent Transformation Consulting - IBM") we have been helping clients set up an evaluation process for bias and other areas. As AI adoption scales and innovations evolve, so will the security guidance mature, as is the case with every technology that’s been embedded into the fabric of an enterprise across the years. Below, we share some best practices from IBM to help organizations prepare for the secure deployment of AI across their environments:

1. Leverage trusted AI by evaluating vendor policies and practices.
    
2. Enable secure access to users, models and data.
    
3. Safeguard AI models, data and infrastructure from adversarial attacks.
    
4. Implement data privacy protection in the training, testing and operations phases.
    
5. Conduct threat modeling and secure coding practices into the AI dev lifecycle.
    
6. Perform threat detection and response for AI applications and infrastructure.
    
7. Assess and decide AI maturity through the [IBM AI framework.](https://www.ibm.com/impact/ai-ethics "AI Ethics - IBM")
    

_To view this article in its original formatting on IBM's website,_ [_click here_](https://www.ibm.com/blog/shedding-light-on-ai-bias-with-real-world-examples/ "Shedding light on AI bias with real world examples - IBM").