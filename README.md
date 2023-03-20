import React from "react";
import ReactDOM from "react-dom";
import FormControlLabel from "@material-ui/core/FormControlLabel";
import TextField from "@material-ui/core/TextField";
import Switch from "@material-ui/core/Switch";
import MUIDataTable from "mui-datatables";
import Cities from "./cities";

class Example extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      data: [
        ["Gabby George", "Business Analyst", "Minneapolis", 30, "$100,000"],
        ["Aiden Lloyd", "Business Consultant", "Dallas",  55, "$200,000"],
        ["Jaden Collins", "Attorney", "Santa Ana", 27, "$500,000"],
        ["Franky Rees", "Business Analyst", "St. Petersburg", 22, "$50,000"],
        ["Aaren Rose", "Business Consultant", "Toledo", 28, "$75,000"],
        ["Blake Duncan", "Business Management Analyst", "San Diego", 65, "$94,000"],
        ["Frankie Parry", "Agency Legal Counsel", "Jacksonville", 71, "$210,000"],
        ["Lane Wilson", "Commercial Specialist", "Omaha", 19, "$65,000"],
        ["Robin Duncan", "Business Analyst", "Los Angeles", 20, "$77,000"],
        ["Mel Brooks", "Business Consultant", "Oklahoma City", 37, "$135,000"],
        ["Harper White", "Attorney", "Pittsburgh", 52, "$420,000"],
        ["Kris Humphrey", "Agency Legal Counsel", "Laredo", 30, "$150,000"],
        ["Frankie Long", "Industrial Analyst", "Austin", 31, "$170,000"],
        ["Brynn Robbins", "Business Analyst", "Norfolk", 22, "$90,000"],
        ["Justice Mann", "Business Consultant", "Chicago", 24, "$133,000"],
        ["Addison Navarro", "Business Management Analyst", "New York", 50, "$295,000"],
        ["Jesse Welch", "Agency Legal Counsel", "Seattle", 28, "$200,000"],
        ["Eli Mejia", "Commercial Specialist", "Long Beach", 65, "$400,000"],
        ["Gene Leblanc", "Industrial Analyst", "Hartford", 34, "$110,000"],
        ["Danny Leon", "Computer Scientist", "Newark", 60, "$220,000"],
        ["Lane Lee", "Corporate Counselor", "Cincinnati", 52, "$180,000"],
        ["Jesse Hall", "Business Analyst", "Baltimore", 44, "$99,000"],
        ["Danni Hudson", "Agency Legal Counsel", "Tampa", 37, "$90,000"],
        ["Terry Macdonald", "Commercial Specialist", "Miami", 39, "$140,000"],
        ["Justice Mccarthy", "Attorney", "Tucson", 26, "$330,000"],
        ["Silver Carey", "Computer Scientist", "Memphis", 47, "$250,000" ],
        ["Franky Miles", "Industrial Analyst", "Buffalo", 49, "$190,000"],
        ["Glen Nixon", "Corporate Counselor", "Arlington", 44, "$80,000"],
        ["Gabby Strickland", "Business Process Consultant", "Scottsdale", 26, "$45,000"],
        ["Mason Ray", "Computer Scientist", "San Francisco", 39, "$142,000"]
      ]
    };
  }

  render() {
    const columns = [
      {
        name: "Delete",
        options: {
          filter: true,
          sort: false,
          empty: true,
          customBodyRender: (value, tableMeta, updateValue) => {
            return (
              <button onClick={() => {
                const { data } = this.state;
                data.shift();
                this.setState({ data });
              }}>
                Delete
              </button>
            );
          }
        }
      },
      {
        name: "Edit",
        options: {
          filter: true,
          sort: false,
          empty: true,
          customBodyRender: (value, tableMeta, updateValue) => {
            return (
              <button onClick={() => window.alert(`Clicked "Edit" for row ${tableMeta.rowIndex}`)}>
                Edit
              </button>
            );
          }
        }
      },
      {
        name: "Name",
        options: {
          filter: true,
        }
      },
      {
        label: "Modified Title Label",
        name: "Title",
        options: {
          filter: true,
        }
      },
      {
        name: "Location",
        options: {
          filter: false,
        }
      },
      {
        name: "Age",
        options: {
          filter: true,
        }
      },
      {
        name: "Salary",
        options: {
          filter: true,
          sort: false,
        }
      },
      {
        name: "Add",
        options: {
          filter: true,
          sort: false,
          empty: true,
          customBodyRender: (value, tableMeta, updateValue) => {
            return (
              <button onClick={() => {
                const { data } = this.state;
                data.unshift(["Mason Ray", "Computer Scientist", "San Francisco", 39, "$142,000"]);
                this.setState({ data });
              }}>
                Add
              </button>
            );
          }
        }
      },
    ];

    const data1 = [
      {Name: "Gabby George", Title: "Business Analyst", Location: "Minneapolis", Age: 30, Salary: "$100,000"},
      {Name: "Aiden Lloyd", Title: "Business Consultant", Location: "Dallas", Age: 55, Salary: "$200,000"},
      {Name: "Jaden Collins", Title: "Attorney", Location: "Santa Ana", Age: 27, Salary: "$500,000"},
      {Name: "Franky Rees", Title: "Business Analyst", Location: "St. Petersburg", Age: 22, Salary: "$50,000"},
      {Name: "Aaren Rose", Title: "Business Consultant", Location: "Toledo", Age: 28, Salary: "$75,000"},
      {Name: "Blake Duncan", Title: "Business Management Analyst", Location: "San Diego", Age: 65, Salary: "$94,000"},
      {Name: "Frankie Parry", Title: "Agency Legal Counsel", Location: "Jacksonville", Age: 71, Salary: "$210,000"},
      {Name: "Lane Wilson", Title: "Commercial Specialist", Location: "Omaha", Age: 19, Salary: "$65,000"},
      {Name: "Robin Duncan", Title: "Business Analyst", Location: "Los Angeles", Age: 20, Salary: "$77,000"},
      {Name: "Mel Brooks", Title: "Business Consultant", Location: "Oklahoma City", Age: 37, Salary: "$135,000"},
      {Name: "Harper White", Title: "Attorney", Location: "Pittsburgh", Age: 52, Salary: "$420,000"},
      {Name: "Kris Humphrey", Title: "Agency Legal Counsel", Location: "Laredo", Age: 30, Salary: "$150,000"},
      {Name: "Frankie Long", Title: "Industrial Analyst", Location: "Austin", Age: 31, Salary: "$170,000"},
      {Name: "Brynn Robbins", Title: "Business Analyst", Location: "Norfolk", Age: 22, Salary: "$90,000"},
      {Name: "Justice Mann", Title: "Business Consultant", Location: "Chicago", Age: 24, Salary: "$133,000"},
      {Name: "Addison Navarro", Title: "Business Management Analyst", Location: "New York", Age: 50, Salary: "$295,000"},
      {Name: "Jesse Welch", Title: "Agency Legal Counsel", Location: "Seattle", Age: 28, Salary: "$200,000"},
      {Name: "Eli Mejia", Title: "Commercial Specialist", Location: "Long Beach", Age: 65, Salary: "$400,000"},
      {Name: "Gene Leblanc", Title: "Industrial Analyst", Location: "Hartford", Age: 34, Salary: "$110,000"},
      {Name: "Danny Leon", Title: "Computer Scientist", Location: "Newark", Age: 60, Salary: "$220,000"},
      {Name: "Lane Lee", Title: "Corporate Counselor", Location: "Cincinnati", Age: 52, Salary: "$180,000"},
      {Name: "Jesse Hall", Title: "Business Analyst", Location: "Baltimore", Age: 44, Salary: "$99,000"},
      {Name: "Danni Hudson", Title: "Agency Legal Counsel", Location: "Tampa", Age: 37, Salary: "$90,000"},
      {Name: "Terry Macdonald", Title: "Commercial Specialist", Location: "Miami", Age: 39, Salary: "$140,000"},
      {Name: "Justice Mccarthy", Title: "Attorney", Location: "Tucson", Age: 26, Salary: "$330,000"},
      {Name: "Silver Carey", Title: "Computer Scientist", Location: "Memphis", Age: 47, Salary: "$250,000" },
      {Name: "Franky Miles", Title: "Industrial Analyst", Location: "Buffalo", Age: 49, Salary: "$190,000"},
      {Name: "Glen Nixon", Title: "Corporate Counselor", Location: "Arlington", Age: 44, Salary: "$80,000"},
      {Name: "Gabby Strickland", Title: "Business Process Consultant", Location: "Scottsdale", Age: 26, Salary: "$45,000"},
      {Name: "Mason Ray", Title: "Computer Scientist", Location: "San Francisco", Age: 39, Salary: "$142,000"}
    ];

    const options = {
      filter: true,
      filterType: 'dropdown',
      responsive: 'stacked',
      page: 2,
      onColumnSortChange: (changedColumn, direction) => console.log('changedColumn: ', changedColumn, 'direction: ', direction),
      onChangeRowsPerPage: numberOfRows => console.log('numberOfRows: ', numberOfRows),
      onChangePage: currentPage => console.log('currentPage: ', currentPage)
    };

    return (
      <MUIDataTable title={"ACME Employee list"} data={this.state.data} columns={columns} options={options} />
    );

  }

}

const rootElement = document.getElementById("root");
ReactDOM.render(<Example />, rootElement);






 Frontend Mentor - Huddle landing page with alternating feature blocks

![Design preview for the Huddle landing page with alternating feature blocks coding challenge](./design/desktop-preview.jpg)

## Welcome! 👋

Thanks for checking out this front-end coding challenge.

[Frontend Mentor](https://www.frontendmentor.io) challenges allow you to improve your skills in a real-life workflow.

**To do this challenges, you need a basic understanding of HTML and CSS.**

## Where to find everything

Your task is to build out the project to the designs inside the `/design` folder. You will find both a mobile and a desktop version of the design to work to. 

The designs are in JPG static format. This will mean that you'll need to use your best judgment for styles such as `font-size`, `padding` and `margin`. This should help train your eye to perceive differences in spacings and sizes.

If you would like the Sketch file in order to inspect the design in more detail you can [subscribe as a PRO member](https://www.frontendmentor.io/pro).

You will find all the required assets in the `/images` folder. The assets are already optimized.

There is also a `style-guide.md` file, which contains the information you'll need, such as color palette and fonts.

## Building your project

Feel free to use any workflow that you feel comfortable with. Below is a suggested process, but do not feel like you need to follow these steps:

1. Initialize your project as a public repository on [GitHub](https://github.com/). This will make it easier to share your code with the community if you need some help. If you're not sure how to do this, [have a read through of this Try Git resource](https://try.github.io/).
2. Configure your repository to publish your code to a URL. This will also be useful if you need some help during a challenge as you can share the URL for your project with your repo URL. There are a number of ways to do this, but we recommend using [Vercel](https://bit.ly/fem-vercel). We've got more information about deploying your project with Vercel below.
3. Look through the designs to start planning out how you'll tackle the project. This step is crucial to help you think ahead for CSS classes that you could create to make reusable styles.
4. Before adding any styles, structure your content with HTML. Writing your HTML first can help focus your attention on creating well-structured content.
5. Write out the base styles for your project, including general content styles, such as `font-family` and `font-size`.
6. Start adding styles to the top of the page and work down. Only move on to the next section once you're happy you've completed the area you're working on.

## Deploying your project

As mentioned above, there are a number of ways to host your project for free. We recommend using [Vercel](https://bit.ly/fem-vercel) as it's an amazing service and extremely simple to get set up with. If you'd like to use Vercel, here are some steps to follow to get started:

1. [Sign up to Vercel](https://bit.ly/fem-vercel-signup) and go through the onboarding flow, ensuring your GitHub account is connected by using their [Vercel for GitHub](https://vercel.com/docs/v2/git-integrations/vercel-for-github) integration.
2. Connect your project to Vercel from the ["Import project" page](https://vercel.com/import), using the "From Git Repository" button and selecting the project you want to deploy.
3. Once connected, every time you `git push`, Vercel will create a new [deployment](https://vercel.com/docs/v2/platform/deployments) and the deployment URL will be shown on your [Dashboard](https://vercel.com/dashboard). You will also receive an email for each deployment with the URL.

## Sharing your solution

There are multiple places you can share your solution:

1. Submit it on the platform so that other users will see your solution on the site. Here's our ["Complete guide to submitting solutions"](https://medium.com/frontend-mentor/a-complete-guide-to-submitting-solutions-on-frontend-mentor-ac6384162248) to help you do that.
2. Share your solution page in the **#finished-projects** channel of the [Slack community](https://www.frontendmentor.io/slack).
3. Tweet [@frontendmentor](https://twitter.com/frontendmentor) and mention **@frontendmentor** including the repo and live URLs in the tweet. We'd love to take a look at what you've built and help share it around.

## Giving feedback

Feedback is always welcome, so if you have any to give on this challenge please email hi[at]frontendmentor[dot]io.

This challenge is completely free. Please share it with anyone who will find it useful for practice.

**Have fun building!** 🚀

## Community Sponsors

A massive thank you to our community sponsors!

- [Zero to Mastery](https://bit.ly/fem-ztm) is an incredible learning resource for all things web development. Led by Andrei Neagoie, the courses are really high-quality content and cover a wide range of in-demand skills.
- [Diversify Tech](https://bit.ly/fem-diversify-tech) is an amazing resource for underrepresented people in tech. The site features job listings for anyone seeking new opportunities. The resource section is also full of useful links to dive into!
- [Triplebyte](http://bit.ly/fem-triplebyte) is a really nice offering if you're looking for a new role. It's a free service that lets you take a confidential quiz. Based on your results companies will pitch you for their vacant roles!
