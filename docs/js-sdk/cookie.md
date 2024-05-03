## $cookie 的定义
*************
public async get(url: string, name?: string): Promise<any>

public async set(
  url: string,
  name: string,
  value: string,
  options: {
    path?: string;
    domain?: string;
    expiresDate?: number;
    maxAge?: number;
    isSecure?: boolean;
    isHttpOnly?: boolean;
    sameSite?: 'Strict' | 'Lax' | 'None';
  } = {},
): Promise<boolean>
