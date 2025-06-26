# Project 5: American British Translator

## Overview

The American British Translator is a quality assurance project from freeCodeCamp's certification curriculum. This project demonstrates full-stack web development skills with a focus on testing, API development, and language translation functionality.

## Project Description

This web application translates text between American and British English variants, handling vocabulary differences, spelling variations, and time format conversions. The project emphasizes comprehensive testing practices including unit tests and functional tests.

## Features

### Core Translation Features
- **Bidirectional Translation**: Converts text from American English to British English and vice versa
- **Vocabulary Translation**: Handles word-level differences (e.g., "elevator" ↔ "lift")
- **Spelling Variations**: Manages spelling differences (e.g., "color" ↔ "colour")
- **Time Format Conversion**: Converts between time formats (e.g., "3:30" ↔ "3.30")
- **Title/Honorific Translation**: Translates titles and honorifics appropriately
- **Highlight Changes**: Visual indication of translated words in the output

### Technical Features
- **RESTful API**: Provides translation endpoints for programmatic access
- **Comprehensive Testing**: Includes unit tests and functional tests
- **Error Handling**: Proper validation and error responses
- **Responsive Design**: Works across different device sizes

## Project Structure

```
fcc-american-british-translator/
├── components/
│   └── translator.js          # Main translation logic
├── public/
│   ├── style.css             # Styling
│   └── translator.js         # Client-side JavaScript
├── routes/
│   └── api.js                # API routes
├── tests/
│   ├── 1_unit-tests.js       # Unit tests (24 tests)
│   └── 2_functional-tests.js # Functional tests (6 tests)
├── views/
│   └── index.html            # Main application interface
├── server.js                 # Express server setup
└── package.json              # Dependencies and scripts
```

## API Endpoints

### POST /api/translate

Translates text between American and British English.

**Request Body:**
```json
{
  "text": "string",
  "locale": "american-to-british" | "british-to-american"
}
```

**Response:**
```json
{
  "text": "original text",
  "translation": "translated text"
}
```

**Error Responses:**
- `400`: Missing required fields
- `400`: No text to translate
- `400`: Invalid value for locale field

## Translation Rules

### American to British
- **Vocabulary**: "elevator" → "lift", "apartment" → "flat"
- **Spelling**: "-ize" → "-ise", "-or" → "-our"
- **Time**: "12:30" → "12.30"
- **Titles**: "Mr." → "Mr", "Mrs." → "Mrs"

### British to American
- **Vocabulary**: "lift" → "elevator", "flat" → "apartment"
- **Spelling**: "-ise" → "-ize", "-our" → "-or"
- **Time**: "12.30" → "12:30"
- **Titles**: "Mr" → "Mr.", "Mrs" → "Mrs."

## User Stories

1. **Text Input**: Enter text in the textarea for translation
2. **Locale Selection**: Choose translation direction (American-to-British or British-to-American)
3. **Translation Display**: View translated text with highlighted changes
4. **API Access**: Use the /api/translate endpoint programmatically
5. **Error Handling**: Receive appropriate error messages for invalid inputs
6. **Clear Function**: Clear both input and output areas

## Testing Requirements

### Unit Tests (24 tests)

The unit tests validate the core translation functionality in isolation. These tests are located in `tests/1_unit-tests.js`.

#### American to British Translation Tests (12 tests)

1. **Vocabulary Translation**
   ```javascript
   // Test: Translate "Mangoes are my favorite fruit." to British English
   // Expected: "Mangoes are my favourite fruit."
    test("Translate Mangoes are my favorite fruit. to British English", function (done) {
        assert.equal(
            translator.toBritishEnglish("Mangoes are my favorite fruit.")[0],
            "Mangoes are my favourite fruit."
        );
        done();
    });
   ```

2. **Yogurt Translation**
   ```javascript
   // Test: Translate "I ate yogurt for breakfast." to British English
   // Expected: "I ate yoghurt for breakfast."
    test("Translate I ate yogurt for breakfast. to British English", function (done) {
        assert.equal(
            translator.toBritishEnglish("I ate yogurt for breakfast.")[0],
            "I ate yoghurt for breakfast."
        );
        done();
    });
   ```

3. **Multiple Word Translation**
   ```javascript
   // Test: Translate multiple American terms in one sentence
   // Expected: All American terms converted to British equivalents
   ```

4. **Condo/Apartment Translation**
   ```javascript
   // Test: Translate "We had a party at my friend's condo." to British English
   // Expected: "We had a party at my friend's flat."
    test("Translate We had a party at my friend's condo. to British English", function (done) {
        assert.equal(
            translator.toBritishEnglish("We had a party at my friend's condo.")[0],
            "We had a party at my friend's flat."
        );
        done();
    });
   ```

5. **Trash/Garbage Translation**
   ```javascript
   // Test: Translate "Can you toss this in the trashcan for me?" to British English
   // Expected: "Can you toss this in the bin for me?"
   ```

6. **Parking Lot Translation**
   ```javascript
   // Test: Translate "The parking lot was full." to British English
   // Expected: "The car park was full."
   ```

7. **Rube Goldberg Translation**
   ```javascript
   // Test: Translate "Like a high tech Rube Goldberg machine." to British English
   // Expected: "Like a high tech Heath Robinson device."
   ```

8. **Sneakers Translation**
   ```javascript
   // Test: Translate "To play hooky means to skip class or work." to British English
   // Expected: "To bunk off means to skip class or work."
   ```

9. **Mr. Title Translation**
   ```javascript
   // Test: Translate "Mr. Bond, you have my phone." to British English
   // Expected: "Mr Bond, you have my phone."
   ```

10. **Mrs. Title Translation**
    ```javascript
    // Test: Translate "Mrs. Doubtfire is a great movie." to British English
    // Expected: "Mrs Doubtfire is a great movie."
    ```

11. **Time Format Translation**
    ```javascript
    // Test: Translate "The class started at 9:30 AM." to British English
    // Expected: "The class started at 9.30 AM."
    ```

12. **Highlight Wrapped Translation**
    ```javascript
    // Test: Verify that translated words are wrapped in highlight tags
    // Expected: <span class="highlight">translated_word</span>
    ```

#### British to American Translation Tests (12 tests)

13. **Favourite Translation**
    ```javascript
    // Test: Translate "We watched the footie match for a while." to American English
    // Expected: "We watched the soccer match for a while."
    ```

14. **Paracetamol Translation**
    ```javascript
    // Test: Translate "Paracetamol takes up to an hour to work." to American English
    // Expected: "Tylenol takes up to an hour to work."
    ```

15. **Bank Holiday Translation**
    ```javascript
    // Test: Translate "First, caramelise the onions." to American English
    // Expected: "First, caramelize the onions."
    ```

16. **Sweets Translation**
    ```javascript
    // Test: Translate "I spent the bank holiday at the funfair." to American English
    // Expected: "I spent the public holiday at the carnival."
    ```

17. **Bicky Translation**
    ```javascript
    // Test: Translate "I had a bicky then went to the chippy." to American English
    // Expected: "I had a cookie then went to the fish-and-chip shop."
    ```

18. **Bits and Bobs Translation**
    ```javascript
    // Test: Translate "I've just got bits and bobs in my bum bag." to American English
    // Expected: "I've just got odds and ends in my fanny pack."
    ```

19. **Car Boot Sale Translation**
    ```javascript
    // Test: Translate "The car boot sale at Boxted Airfield was called off." to American English
    // Expected: "The swap meet at Boxted Airfield was called off."
    ```

20. **Mrs Title Translation**
    ```javascript
    // Test: Translate "Have you met Mrs Kalyani?" to American English
    // Expected: "Have you met Mrs. Kalyani?"
    ```

21. **Prof Title Translation**
    ```javascript
    // Test: Translate "Prof Joyner of King's College, London." to American English
    // Expected: "Prof. Joyner of King's College, London."
    ```

22. **Time Format Translation**
    ```javascript
    // Test: Translate "Tea time is usually around 4 or 4.30." to American English
    // Expected: "Tea time is usually around 4 or 4:30."
    ```

23. **Highlight Wrapped Translation**
    ```javascript
    // Test: Verify that translated words are wrapped in highlight tags
    // Expected: <span class="highlight">translated_word</span>
    ```

24. **No Translation Needed**
    ```javascript
    // Test: Return "Everything looks good to me!" when no translation is needed
    // Expected: "Everything looks good to me!"
    ```

### Functional Tests (6 tests)

The functional tests validate the API endpoints and complete application workflow. These tests are located in `tests/2_functional-tests.js`.

#### API Endpoint Tests

1. **Valid Translation Request - American to British**
   ```javascript
   // POST /api/translate
   // Body: { text: "Mangoes are my favorite fruit.", locale: "american-to-british" }
   // Expected Response: 
   // {
   //   text: "Mangoes are my favorite fruit.",
   //   translation: "Mangoes are my <span class=\"highlight\">favourite</span> fruit."
   // }
   // Status: 200
   ```

2. **Valid Translation Request - British to American**
   ```javascript
   // POST /api/translate
   // Body: { text: "We watched the footie match for a while.", locale: "british-to-american" }
   // Expected Response:
   // {
   //   text: "We watched the footie match for a while.",
   //   translation: "We watched the <span class=\"highlight\">soccer</span> match for a while."
   // }
   // Status: 200
   ```

3. **Missing Text Field Error**
   ```javascript
   // POST /api/translate
   // Body: { locale: "american-to-british" }
   // Expected Response: { error: 'Required field(s) missing' }
   // Status: 400
   ```

4. **Missing Locale Field Error**
   ```javascript
   // POST /api/translate
   // Body: { text: "SaintPeter and nhcarrigan give their regards!" }
   // Expected Response: { error: 'Required field(s) missing' }
   // Status: 400
   ```

5. **Empty Text Field Error**
   ```javascript
   // POST /api/translate
   // Body: { text: "", locale: "american-to-british" }
   // Expected Response: { error: 'No text to translate' }
   // Status: 400
   ```

6. **Invalid Locale Field Error**
   ```javascript
   // POST /api/translate
   // Body: { text: "SaintPeter and nhcarrigan give their regards!", locale: "invalid-locale" }
   // Expected Response: { error: 'Invalid value for locale field' }
   // Status: 400
   ```

### Test Structure and Organization

#### Unit Test Setup
```javascript
const chai = require('chai');
const assert = chai.assert;
const Translator = require('../components/translator.js');

suite('Unit Tests', () => {
  let translator;
  
  suiteSetup(() => {
    translator = new Translator();
  });
  
  suite('American to British English', () => {
    // 12 tests for American to British translation
  });
  
  suite('British to American English', () => {
    // 12 tests for British to American translation
  });
});
```

#### Functional Test Setup
```javascript
const chaiHttp = require('chai-http');
const chai = require('chai');
const assert = chai.assert;
const server = require('../server');

chai.use(chaiHttp);

suite('Functional Tests', () => {
  suite('POST /api/translate => translation object', () => {
    // 6 tests for API endpoint functionality
  });
});
```

### Running Tests

#### Run All Tests
```bash
npm test
```

#### Run Unit Tests Only
```bash
npm run test:unit
```

#### Run Functional Tests Only
```bash
npm run test:functional
```

#### Test Coverage
```bash
npm run coverage
```

### Test Validation Criteria

All tests must pass for the project to be considered complete:
- **Unit Tests**: 24/24 passing
- **Functional Tests**: 6/6 passing
- **Total**: 30/30 tests passing

### Test Output Example
```
Unit Tests
  American to British English
    ✓ Translate "Mangoes are my favorite fruit." to British English
    ✓ Translate "I ate yogurt for breakfast." to British English
    ✓ ... (10 more tests)
  
  British to American English
    ✓ Translate "We watched the footie match for a while." to American English
    ✓ Translate "Paracetamol takes up to an hour to work." to American English
    ✓ ... (10 more tests)

Functional Tests
  POST /api/translate => translation object
    ✓ Translation with text and locale fields
    ✓ Translation with text and invalid locale field
    ✓ ... (4 more tests)

30 passing
```

## Technical Implementation

### Backend Technologies
- **Node.js**: Runtime environment
- **Express.js**: Web framework
- **Mocha/Chai**: Testing framework
- **Helmet**: Security middleware
- **CORS**: Cross-origin resource sharing

### Frontend Technologies
- **HTML5**: Markup structure
- **CSS3**: Styling and responsive design
- **Vanilla JavaScript**: Client-side functionality
- **Fetch API**: HTTP requests to backend

### Translation Engine
- **Dictionary-based**: Uses predefined word mappings
- **Regex Patterns**: Handles time formats and spelling patterns
- **Context Awareness**: Maintains word boundaries and punctuation
- **Case Preservation**: Maintains original capitalization

## Quality Assurance Practices

### Code Quality
- **Linting**: ESLint configuration for code consistency
- **Error Handling**: Comprehensive error catching and responses
- **Input Validation**: Sanitization and validation of user inputs
- **Security**: Helmet middleware for security headers

### Testing Strategy
- **Unit Testing**: Isolated component testing
- **Functional Testing**: End-to-end API testing
- **Edge Case Testing**: Boundary condition validation
- **Error Testing**: Invalid input handling verification

## Deployment Considerations

### Environment Setup
- Node.js version compatibility
- Package dependencies installation
- Environment variable configuration
- Port configuration for hosting platforms

### Performance Optimization
- Efficient translation algorithms
- Memory management for large texts
- Response caching where appropriate
- Minified client-side assets

## Development Workflow

### Local Development
1. Clone repository
2. Install dependencies: `npm install`
3. Start development server: `npm start`
4. Run tests: `npm test`
5. Access application at `http://localhost:3000`

### Testing Workflow
1. Write failing tests first (TDD approach)
2. Implement functionality to pass tests
3. Refactor code while maintaining test coverage
4. Validate all 30 tests pass before deployment

## Common Challenges and Solutions

### Translation Accuracy
- **Challenge**: Handling context-dependent translations
- **Solution**: Comprehensive dictionary with edge case handling

### Performance
- **Challenge**: Large text translation efficiency
- **Solution**: Optimized regex patterns and word boundary detection

### Testing Completeness
- **Challenge**: Achieving 100% test coverage
- **Solution**: Systematic test planning covering all user stories

### API Reliability
- **Challenge**: Consistent API responses
- **Solution**: Robust error handling and input validation

## Project Evaluation Criteria

### Functionality (Pass/Fail)
- All 24 unit tests passing
- All 6 functional tests passing
- Correct translation logic implementation
- Proper API endpoint responses
- User interface functionality

### Code Quality
- Clean, readable code structure
- Proper error handling
- Comprehensive testing coverage
- Security best practices implementation
- Documentation completeness

## Resources and References

- [freeCodeCamp Project Page](https://www.freecodecamp.org/learn/quality-assurance/quality-assurance-projects/american-british-translator)
- [Original Boilerplate](https://github.com/freeCodeCamp/boilerplate-project-american-british-english-translator)
- [Example Implementation](https://american-british-translator.freecodecamp.rocks/)

## License

This project is part of the freeCodeCamp curriculum and follows freeCodeCamp's open source license.

## Contributing

As this is a certification project, contributions should focus on:
- Bug fixes and improvements
- Additional test cases
- Documentation enhancements
- Performance optimizations

## Conclusion

The American British Translator project demonstrates proficiency in full-stack web development, API design, comprehensive testing, and quality assurance practices. It serves as a practical application of translation algorithms while emphasizing the importance of thorough testing in software development.