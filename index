# vulnerable_app.py
from flask import Flask, request, render_template_string

app = Flask(__name__)

# 취약한 로그인 폼 (SQL Injection 가능)
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        email = request.form.get('email')
        password = request.form.get('password')

        # 실제 DB 없이 단순 문자열 비교지만, 시뮬레이션을 위해 SQL 문을 그대로 노출
        query = f"SELECT * FROM users WHERE email = '{email}' AND password = '{password}'"
        print("[!] 실행된 쿼리:", query)

        if email == "' OR 1=1--":
            return "<h1>Login 성공! (SQL Injection)</h1>"
        else:
            return "<h1>Login 실패</h1>"

    return '''
        <form method="post">
            Email: <input name="email"><br>
            Password: <input name="password"><br>
            <button type="submit">Login</button>
        </form>
    '''

# 취약한 검색 (DOM XSS 가능)
@app.route('/search')
def search():
    q = request.args.get('q', '')
    return render_template_string(f'''
        <h1>Search Page</h1>
        <form method="get">
            <input name="q" value="{q}">
            <button type="submit">Search</button>
        </form>
        <p>검색 결과: {q}</p>
    ''')

if __name__ == '__main__':
    app.run(debug=True)
