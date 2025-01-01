import { Client, Account, ID } from "appwrite";
import conf  from '../conf/conf';

// const client = new Client()
//     .setEndpoint(conf.appwriteUrl) // Your API Endpoint
//     .setProject(conf.appwriteProjectId); // Your project ID
//
// const account = new Account(client);
//
// const promise = account.create('[USER_ID]', 'email@example.com', '');
//
// promise.then(function (response) {
//     console.log(response); // Success
// }, function (error) {
//     console.log(error); // Failure
// });

class AuthService {
    client = new Client();
    account;

    constructor() {
        this.client
            .setEndpoint(conf.appwriteUrl) // Your API Endpoint
            .setProject(conf.appwriteProjectId)
        this.account = new Account(this.client);
    }

    async createAccount({email, password, name}) {
       try {
            const userAccount = this.account.create(ID.unique(), email, password, name);
            if (userAccount) {
                // call another method
                return this.login({email, password});
            } else {
                return userAccount;
            }
       } catch (error) {
           console.log(`Error creating account: ${error}`);
       }
    }

    async login({email, password}) {
        try {
            const loggedinAccount = this.account.createEmailPasswordSession(email, password);
            if (!loggedinAccount) {
                // call another method
            } else {
                return loggedinAccount;
            }
        } catch (error) {
            console.log(`Error while logging in account: ${error}`);
        }
    }

    async getCurrentUser() {
        try {
            return await this.account.get();
        } catch (error) {
            console.log(`Appwrite service :: getCurrentUser :: error: ${error}`);
        }

        return null;
    }

    async logout() {
        try {
            return await this.account.deleteSession('current');
        } catch (error) {
            console.log(`Appwrite service :: logout :: error: ${error}`);
        }
    }
}

const authService = new AuthService();

export default authService;
