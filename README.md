describe('Airspace log in', function () {



	it('Verify log in', () => {
		cy.on("uncaught:exception", (err, runnable) => {
			// returning false here prevents Cypress from
			// failing the test
			return false
		})

		// Open log in page
		cy.visit("https://the-internet.herokuapp.com/login")

		//Verify "Login Page" heading
		cy.get('h2').should('be.visible')
			.and('contain', 'Login Page')
			.and('have.css', 'font-size', '37px')
			.and('have.css', 'color', 'rgb(34, 34, 34)')

		//Verify text under heading
		cy.get('.subheader').should('be.visible')
			.and('have.text', "This is where you can log into the secure area. Enter tomsmith for the username and SuperSecretPassword! for the password. If the information is wrong you should see error messages.")

		//Verify Username text
		cy.get(':nth-child(1) > .large-6 > label').should('be.visible')
			.and('have.text', "Username")

		//Verify Password text
		cy.get(':nth-child(2) > .large-6 > label').should('be.visible')
			.and('have.text', "Password")

		//Verify Login button
		cy.get('.radius').should('be.visible')
			.and('contain', 'Login').and('have.css', 'background-color', 'rgb(43, 166, 203)')

			//Test case #1 - Correct username, correct password
		//Type correct username "tomsmith"
		cy.get('#username').type('tomsmith')

		//Type correct password "SuperSecretPassword!"
		cy.get('#password').type('SuperSecretPassword!')

		//Click Login button
		cy.get('button.radius').click()

		//Verify successful login
		cy.get('.flash').should('be.visible')
			.and('have.attr', 'class', 'flash success')
			.and('contain', "You logged into a secure area!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(93, 164, 35)')

		//Verify "Secure area' text
		cy.get('h2').should('be.visible')
			.and('have.text', " Secure Area")
			.and('have.css', 'color', 'rgb(34, 34, 34)')

		//Verify subheader text 	
		cy.get('h4').should('be.visible')
			.and('have.text', "Welcome to the Secure Area. When you are done click logout below.")
			.and('have.css', 'color', 'rgb(111, 111, 111)')

		//Verify Logout button
		cy.get('.button').should('be.visible')
			.and('have.attr', 'href', '/logout')
			.and('contain', 'Logout').and('have.css', 'color', 'rgb(51, 51, 51)')

		//Click Logout button
		cy.get('.button').click()

		//Verify Logout message
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash success')
			.and('contain', "You logged out of the secure area!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(93, 164, 35)')

			//Test case #2 - blank username, blank password
		//Leave username and password blank
		//Click Login button
		cy.get('button.radius').click()

		//Verify login error message Your username is invalid! 
		//Note: I don't have requirements, but if the requirement is the message to say "Your username and password are invalid!" then this step fails.
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash error')
			.and('contain', "Your username is invalid!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(198, 15, 19)')

			//Test case #3 - blank username, correct password
		//Leave username blank

		//Type correct password "SuperSecretPassword!"
		cy.get('#password').type('SuperSecretPassword!')

		//Click Login button
		cy.get('button.radius').click()

		//Verify login error message Your username is invalid! 
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash error')
			.and('contain', "Your username is invalid!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(198, 15, 19)')

			//Test case #4 - correct username, blank password
		//Type correct username "tomsmith"
		cy.get('#username').type('tomsmith')

		//Leave password blank

		//Click Login button
		cy.get('button.radius').click()

		//Verify login error message Your password is invalid! 
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash error')
			.and('contain', "Your password is invalid!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(198, 15, 19)')

			//Test case #5 - correct username, incorrect password
		//Type correct username "tomsmith"
		cy.get('#username').type('tomsmith')

		//Type incorrect password "IncorrectPassword!"
		cy.get('#password').type('IncorrectPassword!')

		//Click Login button
		cy.get('button.radius').click()

		//Verify login error message Your password is invalid! 
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash error')
			.and('contain', "Your password is invalid!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(198, 15, 19)')

			//Test case #6 - incorrect username, correct password
		//Type incorrect username "smith"
		cy.get('#username').type('smith')

		//Type correct password "SuperSecretPassword!"
		cy.get('#password').type('SuperSecretPassword!')

		//Click Login button
		cy.get('button.radius').click()

		//Verify login error message Your username is invalid! 
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash error')
			.and('contain', "Your username is invalid!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(198, 15, 19)')

			//Test case #7 - incorrect username, incorrect password
		//Type incorrect username "smith"
		cy.get('#username').type('smith')

		//Type incorrect password "IncorrectPassword!"
		cy.get('#password').type('IncorrectPassword!')

		//Click Login button
		cy.get('button.radius').click()

		//Verify login error message Your username is invalid!
		//Note: I don't have requirements, but if the requirement is the message to say "Your username and password are invalid!" then this step fails.
		cy.get('#flash').should('be.visible')
			.and('have.attr', 'class', 'flash error')
			.and('contain', "Your username is invalid!")
			.and('have.css', 'color', 'rgb(255, 255, 255)')
			.and('have.css', 'background-color', 'rgb(198, 15, 19)')


	})
})
