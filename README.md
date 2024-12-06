# React-restful
React.js communication RESTful API webservice

<p align="center" width="100%">
    <img width="25%" src="https://github.com/jkaewprateep/React-restful/blob/main/Reacts.jpg">
    <img width="25%" src="https://github.com/jkaewprateep/React-restful/blob/main/RestfulAPI.jpg">
    <img width="15%" src="https://github.com/jkaewprateep/React-restful/blob/main/kid44.jpg"> </br> 
    <b> React communication webservice </b> </br>
    <b> ( Picture from Internet ) </b> </br>
</p>

🧸💬 With real-time statistics, source code access, reliable format, and customizable Reacts.js is one option for web applications and dashboards when communications requirements are developed ```single method communication``` makes it easier to manage both cascade stylesheet, source codes, integration method, and user accessibilities. </br>
🐯💬 Culture INFO, in some countries ```stylesheets are also intellectual property``` of the project because they develop all their source codes and version control them, download and distribution for the same organized project is an application for some sources. Hiring one project and including source codes in another project is not an application but when resources are limited allows for the initial start project and development phase. ( Existing source codes are used for development only and they have work hours because blend from programmer experience ) </br>
🦁💬 Project development has objectives that need to include ```stylesheets and UI design```, and the main functions program or individual are the main objective because they are included in most project objectives and stylesheets, seem to be a cosmetic path or have budget control, project resources had budget control but not in the objective is hiring purchase. </br>

```
import '../../App.css';
import './table.css';

//
import React, { useEffect, useState } from 'react';
import axios from 'axios'

//
import moment from 'moment-timezone';

function DateDiff(datetime) {
    const timenow = moment(new Date());
    const newtime = moment(datetime);
    const days = moment.duration(timenow.diff(newtime)).days();
    const hours = moment.duration(timenow.diff(newtime)).hours();
    const minutes = moment.duration(timenow.diff(newtime)).minutes();
    const seconds = moment.duration(timenow.diff(newtime)).seconds();

    let new_hour = "";
    if (hours < 9) {
        new_hour = "0" + hours.toString();
    }
    else {
        new_hour = hours.toString();
    }

    let new_minute = "";
    if (minutes < 9) {
        new_minute = "0" + minutes.toString();
    }
    else {
        new_minute = minutes.toString();
    }

    let new_second = "";
    if (seconds < 9) {
        new_second = "0" + seconds.toString();
    }
    else {
        new_second = seconds.toString();
    }

    let new_string = "";
    if (days > 0) {
        new_string = days.toString() + "d: " + new_hour + "-" + new_minute + "-" + new_second;
    }
    else {
        new_string = new_hour + "-" + new_minute + "-" + new_second;
    }

    return new_string;
}

function App() {

    const [searchResults, setSearchResults] = useState([]);
    const [page01_counter, setPage01_counter] = React.useState(60);

    useEffect(() => {
        // fetch all products
        const fetchOrders = async () => {

            let url = "https://localhost:8080/recorddisplay/robot_1";
            // console.log(url)

            const interval = await setInterval(async () => {

                await axios.get(url, {
                    auth: {
                        username: 'robot_1',
                        password: '1234'
                    },
                })
                    .then(async res => await setSearchResults(res.data.slice(0, 10)))
                    .catch(async err => await console.error(err));

            }, 1000); //set your time here. repeat every 1 seconds
            return async () => await clearInterval(interval);
        };
        fetchOrders();
    }, [page01_counter]);


    return (
        <><div class="container">
            User activity
            <table className='ReactTable'>
                <tr text-align='center' colspan="4">
                    <th text-align='center'>Time</th>
                    <th text-align='center'>Status</th>
                    <th text-align='center'>Robotname</th>
                    <th text-align='center'>Useragent</th>
                </tr>
                {
                    searchResults.map((key, idx) => (
                        <tr colspan="4" text-align='left' key={key.id}>
                            <td>{DateDiff(key.responsetime.$date)}</td>
                            <td>{key.type}</td>
                            <td>{key.requester.username}</td>
                            <td>{key.agent_id}</td>
                        </tr>
                    ))
               }
            </table>
        </div ></>
    );
}

export default App;
```
